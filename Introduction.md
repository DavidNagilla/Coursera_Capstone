# Introduction / Business Problem


Problem

The goal of this project is to solve the problem of deciding where a group of people should go eat together. Frequently coworkers and friends wish to eat together, but must make a decision as to where. In order to speed up the process and lower the probability of an argument, we will automate this decision process via a recommendation based on individual preferences using Foursquare data.

Target Audience

The target audience is any individual interested in engaging in the social activity of eating in a large group, whether for pleasure, work, or both. Selecting a dining establishment that can accomodate several individuals' choices at once with minimal friction should be of interest to the average individual in general.

Further Information and Future Plans

We will make the following assumptions for the purposes of simplifying this project:

Individuals will establish a profile in a database containing a list of restaurants that they have ranked as favorable or not (+/- 1). Any restaurant not ranked will be given a neutral score (0).

Users will submit a list of all users that are going to lunch together and a latitude/longitude location to be used for finding a restaurant.

Foursquare will be used to find a list of nearby restaurants.

A group preference list will be established by adding up the ranks of each user in the lunch group for each restaurant listed by Foursquare.

After ordering the list by rank, a random suggestion will be taken by one of the top 8 spots. A random selection will be used to avoid always returning the same restaurant for the same group of people.

In a future version, users should be able to create more complicated profiles, perhaps describing their preferences based on type of cuisine, how much they like/dislike a restaurant (a ranking from -5 to 5, say), past attendance (in case a user has already attended a restaurant in the past week), restaurant grade (in New York) or rating, etc.
