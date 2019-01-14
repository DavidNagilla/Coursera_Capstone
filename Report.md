# Introduction

The goal of this project is to solve the problem of deciding where a group of people should go eat together. Frequently coworkers and friends wish to eat together, but must make a decision as to where. In order to speed up the process and lower the probability of an argument, we will automate this decision process via a recommendation based on individual preferences using Foursquare data.
The target audience is any individual interested in engaging in the social activity of eating in a large group, whether for pleasure, work, or both. Selecting a dining establishment that can accommodate several individuals' choices at once with minimal friction should be of interest to the average individual, in general.

# Data

In order to complete this project, we will need two major sources of data:
A database containing user profiles with their restaurant preferences. For now, users will have a name, a list of restaurants they enjoy, and a list of restaurants they wish to avoid. (A future version could eventually allow for a more complex profile.)
The Foursquare location data to help find a restaurant. (A future version could make use of a restaurants rating to help select a location.)

In a future version, a third dataset would be useful for New York users:
The NYC Open Data webpage contains a listing of restaurant grades given by the city. This could be used to select restaurants with a minimum grade score.

A very basic example of user data:

User	James
Likes	Taco House 39, Chen's Garden, Pho Viet
Dislikes	Pizza Hut, La Sorrentina

# Methodology

Since no database currently contains our desired dataset on user restaurant preferences, we created one for 20 randomly generated users each having a profile with 15 local restaurants that they enjoy and 15 that they do not.
In order to make a recommendation, a group of users that are going to eat together needs to be selected from the overall user dataset. Once a group is selected, Foursquare is queried for a list of restaurants that are near the group's location. The result of the query is stored as a list.
We now begin constructing a dictionary where the keys are the restaurants from our Foursquare query and the values are the sum of the user preferences for that restaurant (a user contributes a 1 if they like it, -1 if they do not, and 0 if the restaurant does not appear anywhere in the user profile).
Once the dictionary is constructed, it can be converted into a dataframe. Restaurants are then ordered by the sum of the user preferences. A random restaurant is selected from the top 8 choices (otherwise the utility will generate the same restaurant if the group and user preferences remain static) to introduce variety.
We also have a method for determining the compatibility of two users. We can create a dictionary of restaurants that have been rated by both users. For each such restaurant we take the product of the user preferences, add up the values, and normalize. This is equivalent to taking a dot product of two vectors. Values close to 1 indicate the both users have similar preferences (it implies that both rated several restaurants the same way). This could be used to make restaurant recommendations based on other user preferences. This is an example of collaborative filtering.

# Results and Discussion

The output of any run in our utility is a single restaurant. This restaurant has been selected at random from a short list of the restaurants that are the most popular among the currently selected lunch group. While the output is simply a single item, the discussion in the Methodology section shows that this output has been produced by carefully considering the preferences of all users in a lunch group.
In our examples below we also compute the compatibility between user0 and all other users. This can be used to make a recommendation for a restaurant that user0 may like/dislike based on other user preferences.

# Conclusion

Arrow's Theorem suggests that unless a lunch group is deciding where to eat between one of two choices, there is no perfect voting system for selecting an overall winner. Our goal here has been to introduce a system with a simple yet reasonable way to select a restaurant that will please as many people as possible in a lunch group. Clearly this will become more difficult as the group size increases, but we feel that this method is effective for small groups (that is, no more than 6).
In a future version, users should be able to create more complicated profiles, perhaps describing their preferences based on type of cuisine, how much they like/dislike a restaurant (a ranking from -5 to 5, say), past attendance (in case a user has already attended a restaurant in the past week), restaurant grade (in New York) or rating, etc. One should therefore consider this utility as a work in progress.
