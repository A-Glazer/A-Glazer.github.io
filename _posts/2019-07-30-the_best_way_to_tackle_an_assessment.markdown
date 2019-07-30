---
layout: post
title:      "The Best Way to Tackle an Assessment"
date:       2019-07-30 20:09:38 +0000
permalink:  the_best_way_to_tackle_an_assessment
---


For my Rails assessment I was given the following task:

1. Create a scope in the `potential_client` model that returns all the clients that have agreed to a meeting
2. Create a route that will render these clients 
3. Create a link on the `business_service` show page that takes you to the new route

Before starting to write the code, it is important to think about the most systematic way to fulfill the tasks. Here are the steps I would take:

**1. Brainstorming**

The first step to complete the task is brainstorming. I created a list of tasks that need to get done. This list is not ordered, it is merely stating everything so I can create an order afterwards.

1.	A scope method in the `potential_clients` model that lists all the potential clients who agreed to a meeting
2.	A new page in `potential_clients` view that will have all the meetings listed
3.	A method in the `potential_clients` controller that will access the scope and allow it to be shown on the new meetings page
4.	A new route for the meetings page
5.	The scope method information displayed on the meetings page
6.	A link on the `business_service` show page that sends the user to the meetings route created

**2.	Creating an Order **

After creating a list of everything that needs to be done, the next step is to create an order and implement it. 

Here is the order I came up with. 

1.	The first thing I would do is create the method in the `potential_clients` controller that will access the scope. The reason I think this is a good first step is because once the scope is created, I’ll need a page to test if it is working properly. I am going to define the method as “meetings”.

2.	Next I would create the page where that method will send to. The page will be called the same as the method, `meetings.erb`. It will be in views/potential_clients. I am going to put pseudo-text on the page, so I know it is appearing correctly.

3.	The next step would be to create the route. In my routes.rb, I will create a get to ‘/meetings’, so now the page exists. 

4.	Then I will test the new link in the browser to make sure the page is appearing correctly.

5.	Once I confirm that it is appearing correctly, I can work on the scope. The scope will be defined in the `potential_clients` model.

6.	The scope could then be called in the meetings method in the `potential_client` controller.

7.	Now the information from the meetings scope could be printed out on the new meetings page.

8.	Once that is done, the next thing I will do is check to make sure everything is working properly.

9.	If it is, than the last step would be to create a link on the `business_service` show page to the `meetings` page.

10.	Lastly, I would check over the requirements to confirm that they were all completed.


**3.	Writing the code**

Once the order is set, I would implement the code. 

**In summary,** when given a task, the first step should always be brainstorming what needs to be done. This will help achieve the desired results in the most time efficient way. Afterwards, you could put the brainstorm notes in a logical order and then start tackling! Another reason brainstorming and creating an order first is a good idea is because often there is a lot of pressure and anxiety at an interview. By having a clear list, it helps you keep focused on the task that needs to get done in the most efficient way.

