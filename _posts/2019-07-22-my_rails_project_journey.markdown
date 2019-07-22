---
layout: post
title:      "My Rails Project Journey"
date:       2019-07-22 20:25:53 +0000
permalink:  my_rails_project_journey
---


Starting a project is overwhelming. Finishing is rewarding. The process is filled with learning. 

For my Rails project, I wanted to create an app that would be helpful for businesses. I thought of creating a b2b marketing app to help a business keep track of their potential clients. To do this, I created a join table, which makes the business service they are offering the "middle man". This would also allow flexibility for a client to find a business through the service. 

Have I lost you yet? Here is a real to life example.

Let say I own a company called Business Boost. We offer a variety of services; graphic design, web development, and video production. You own a dry cleaning business and could really use an advertisement video. Therefore, we both have the business service "video production" in common.

In this app, the owner will be able to make a list of all the services they offer and the potential clients that may be interested. They can keep track of when they last contacted them, their reply, suggested follow up date, and if they agreed to a meeting. 

In theory, it was working great, but then I ran into a stumbling block. I wanted to list all the business service's potential clients, but I couldn't because the business service was the join table.  

In other words...

It made sense to have the business service as the join table, however a join table means it belongs to a business owner and potential client. In my case though, I needed the business table to both belong to and have many potential clients, which was not allowed. After many trials and errors, I came up with a solution. I created another table called business_service_potential_client. This table became my join table belonging to both the business_service and potential client. Now, the business service table was able to have many potential clients through the join table. 

It may sound simple on paper, but the whole process of coming up with a solution took a lot of thinking and rethinking, and trial and error. Through this process, I feel like I've gained a greater understanding of associations, which has always confused me. Creating an rails application isn't easy, but I feel like I've gained so much from it! 
