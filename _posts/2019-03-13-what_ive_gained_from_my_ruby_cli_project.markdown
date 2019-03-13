---
layout: post
title:      "What I've Gained from my Ruby CLI Project"
date:       2019-03-13 20:28:09 +0000
permalink:  what_ive_gained_from_my_ruby_cli_project
---

The CLI gem project has been a great learning experience for me. It has helped me solidify what I've learned so far and apply it to a different project. I enjoyed reviewing my notes, going back to previous labs, and thinking out of the box in order to solve each error. 

**Challenges**
I found the most challenging part of the project was figuring out how to set up my class. I had to figure out where each class had to be required and how the classes would be connected. I thought of the classes like this: 
Imagine a restaurant with a cook, customer, and food. The Scraper class is the cook. That is where the food is being prepared, or in our case, the website is being scraped. The Flower class is the customer, who receives the final version of all the food. The customer doesn't see what goes on behind the scenes, he just sees the final version. The CLI class is everything in between. This includes the organized scraped information, all the greetings, user inputs, goodbyes, and everything else. 

**How it works**
Before I even began my project, I created a notes file with pseudocode. This helped me figure out what needed to be created, scraped off the webpage, gotten from the user, or organized.
The first method was the scraper method is the Scraper class. It scrapes the website and provides the project with each flower's name, price, and url. Each scraped flower is then saved in the Flower class for further accessed. 
The next step is the he scraper_categories method in the CLI class. The scraper_categories method organizes all the scraped flowers according to price range. Since it is only accessing the information already scraped (not rescraping), it is placed in the CLI class. 
Up until this point there has been no interaction with the user. Now in the greeting method, the user is greeted and asked to choose a price range. I found it fun trying to figure out how to sort by price range and give the user the list of flowers with no duplicates. 
After the user gets the list of flowers within their price range, they are offered to choose a specific flower to see more information. They are given the name, price, and link to view/order it. 
The final step is the goodbye method - thanking the customer for shopping and giving them a choice to view the program from the beginning or exit. 

**After thoughts**
I really enjoyed thinking out of the box to get my code working. I spent many hours playing with binding.pry until I thought it worked, but then didn't. It was so rewarding watching the project break many times and then finally getting it work properly! Pair programming was also a big highlight. When I or a classmate got stuck, we discussed our codes and bounced ideas off of each other. I feel I gained a lot from these interactions.

