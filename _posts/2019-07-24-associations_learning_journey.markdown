---
layout: post
title:      "Associations Learning Journey"
date:       2019-07-24 18:24:14 +0000
permalink:  associations_learning_journey
---


One of the challenges I faced while creating my rails application was associations. The concept of different relationships, `has_many,` `belongs_to`, and `has_many, through` confused me. After a lot of research, mentorship, and trial and error, I  feel like I have gained a much greater understanding. 

**Why should I use associations?**

Associations make coding much simpler. It allows the programmer to connect different models together. The project I created was a B2B Marketing App. The app enables a business owner/user to keep track of potential clients that might benefit from their services. Therefore, it made sense to make the `business service` as the middle-man aka join table. 

However, I ran into a dilemma. 

By definition, a join table `belongs to` the models it is joining. This means that the `business service` could have only one `user` and one `potential client`. The `user` and `potential client` can each have many `business services`. 

<a href="https://ibb.co/Yp3LhN0"><img src="https://i.ibb.co/qkdrpDJ/join-table-relationship.jpg" alt="join-table-relationship" border="0"></a>

I wanted my `user` to have many `business services`, and each `business service` belong to and have many `potential clients`. The user would be able to click on a business service they offer and see all the potential clients they have for that service. But since the `business service` belongs to only one `potential client`, when `business_service.potential_client` is called, it would only return one potential client. 

**So how could I get `business services` to show all `potential clients`?**

After brainstorming through many possibilities, the most DRY method I came up with was to create another join table between `business services` and `potential clients`. This new table, called `business service potential clients` could belong to a `business service` and a `potential client`. Now the `business service` could have many `potential clients` through the `business service potential client` table. I could call `business_service.potential_clients` and it will return all the `potential clients` that belong to the `business service`. 

<a href="https://ibb.co/NT7X0Dh"><img src="https://i.ibb.co/0sQk04N/business-service-potential-client-join-table.jpg" alt="business-service-potential-client-join-table" border="0"></a>


**Now that the associations make sense, how do I define them in the models and database?**

There are a few lines of code I needed to add to create the associations. 

The models class is where the `belongs_to`, `has_many` and `has_many :through` is defined. This is how it would look:

```
class BusinessService < ApplicationRecord
    belongs_to :user
    has_many :business_services_potential_client
    has_many :potential_clients, through: :business_services_potential_client
end
```

```
class BusinessServicesPotentialClient < ApplicationRecord
    belongs_to :potential_client
    belongs_to :business_service
end
```

```
class PotentialClient < ApplicationRecord
    has_many :business_services_potential_client
    has_many :business_services, through: :business_services_potential_client 
end
```

```
class User < ApplicationRecord
    has_many :business_services 
    has_many :potential_clients, through: :business_services
end
```

The database is where the `foreign keys` are added. Any method that belongs to another object, needs to have a foreign id of that object. So, the `business service potential client` table needs to contain a `business service id` and `potential client id`. The `potential clients` table needs to have a `business service id`. This will allow a new `potential client` to be associated with a `business service` right when it is created. 

**When adding `has many` and `belongs to` in the model, should it be singular or plural?**

Think about it logically, a child `belongs to` one mother and one father, while a mother or father could `have many` children. The same works in Rails. When defining `has many` and `belongs to` in the model, `has many` should be plural and `belongs to` should be singular.

**How does `has_many :through` work?**

`has_many :through` contains a middleman. The only way the two models can be connected, is through a third model. Let's use the parent-child-grandchild relationship. Let's say the parent has a grandchild. The only way the parent and grandchild are connected, is through the child. So the child would be the join table (aka: middle man). In the B2B Marketing app, the only way a `user` could have `potential clients` is through a `business service`. Logically, if the company didn't offer any services, they wouldn't have any `potential clients` to reach out to!

I hope the associations are clearer now. The concepts may seem daunting at first, but if you think about them logically, they make a lot of sense!



