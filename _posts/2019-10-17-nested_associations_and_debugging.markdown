---
layout: post
title:      "Nested Associations and Debugging"
date:       2019-10-17 18:55:54 +0000
permalink:  nested_associations_and_debugging
---

For the Rails-JavaScript project, I created a B2B Marketing app, which allows a user to create 1. a business service and 2. potential clients that can benefit from their service. There are 2 main controllers - `business_service` and `potential_client` (there is also a user and session, but those aren't important for this article). They are associated together with a join table called `business_service_potential_client`. This allows `business_service` to have many `potential_clients`.  

One of the difficulties I faced when creating my project was with the `new potential client form`. On the `business service show page`, there is a button to display potential clients and create a new potential client. I created a JavaScript function to display the clients on click and another function to display the clients once the form was submitted. The trouble I faced was the potential client was being created and displayed, but once I refreshed the page, the newly-added client would disappear. 

To solve this issue, I used a lot of `debugger`, `binding.pry`, `console`, and the `terminal`. I examined step by step what was happening. I started from the beginning of the app, looking first at the `business_service index page`. I saw that the business service was successfully appearing and the `new business_service form` was working properly. I tried to copy the working code from the` business_service form` for potential clients (and changing the appropriate details), but it was still giving me an error. 

Next, I clicked the link to the `business service show page` where the `potential_client new form` was located, which loaded properly. I followed along in the terminal and saw that when the potential client was being created, it was using the create method in the `business_service controller`. I figured this out when I typed in `params` in the terminal and saw it was trying to create a new business_service instead of a potential client since it was referring to the wrong create method! 

To simplify everything, I separated the controllers and made a separate `potential_clients.js` and `potential_client controller`, even though they are all appearing on the `business_service` pages. Once I did that, I created an action telling it to use the `potential_client create method` when creating a new potential client. This semi-worked. 

What went wrong? 

To create a new potential_client, the code used in the create method was `PotentialClient.new(client_params)`. When I debugged using `binding.pry`, the potential client was creating properly with all the correct information and saving properly as well. It was missing the `business_service_id`, but I was able to fix that easily by adding the code `@potential_client.business_service_id = @business_service.id`. *Note: This is the first key to what was wrong, why wasn't the business_service_id added automatically!?*

Once I saw that from the Rails side the potential client was being created properly, I moved onto the JavaScript side. There I saw that the potential client was indeed being created and even appearing on the screen, but when I refreshed the page, it would disappear! So I started a `rails console` and saw that the new potential client was there, just not displaying anywhere. 

I was lost as to what to do next. I knew the form was creating the `potential_client` and it was even showing it immediately, yet where was it disappearing to? I went back to my `potential_client controller` and saw that once the potential client was saving, it was rendering it in json. I decided to inspect the json and there I found my error! It seems like the potential_client was not appearing in json on the `business_service show` page. 

In the json file, there was the `business_service` and then all the other `potential_clients` nested under it and their information. Walla! That was the issue. I had never attached the `potential_client` to the `business_service`. (Remember I had to manually add the `business_service_id`). To solve this issue, I changed the create method to `@potential_client = @business_service.potential_clients.new(client_params)`. Now the `potential_client` belonged to the `business_service` and it appeared on the `business_service show` page!

To confirm my theory that it needed to be nested, I realized the only way to get to any `potential_client` page (index, show etc.), is through the `business_service show` page. The route is `/business_services/:business_service_id/potential_clients`. 

This project taught me how to really debug and examine every step of way. I used a lot of `break-points` and `binding.pry` and feel much more confident in debugging! I also got into the habit of reading the terminal to determine exactly what was happening (until now I didn't realize its importance). And lastly, I learned the hard way about associations and the importance of keeping them nested at every step of the process. It wasn't enough to just manually add an id of the correct business_service, it actually had to be created nested under it. 
