---
layout: post
title:      "My Sinatra Project Learning Journey"
date:       2019-05-27 17:32:24 +0000
permalink:  my_sinatra_project_learning_journey
---


Wow I did it! What an accomplishing feeling handing in a project after spending so many hours writing code, debugging, fixing errors, and then all over again! Whenever I thought it worked, another error came up. The fun of programming:)!

I learned so much from this project and I'd like to share some tips I've gained along the way.

In the `application_controller`, a great way to simplify code is to make a `helpers` method where you define the methods that will be reused over and over again. I created 2 methods, the first a `current_user` method, enables the application to find the current user based on the session id. The second method, `is_logged_in?` is to check if the user is logged in. It is very important to check that the user matches the params when they go to a new link, otherwise someone can access another person's shopping list. 

The next step was to set params for the user. The computer isn't smart enough to know what defines a user, therefore I created a users table with columns defining the user. So now when the user signs in, the program will be able to check its params by the columns defined in the user table. 

Once the user table is set up, I created a `user_controller` which controls what happens when the user clicks on certain buttons. The user controller consists of `get` and `post` requests. What is the difference between `get` and `post`? A `get` request is the url that is put into the browser. So  `get '/signup'` would be accessed when the user types in (or links to) `http://127.0.0.1:9393/signup`. The `post` request is the output when the user clicks a link. For example, if the user finishes filling out the signup form and clicks the submit button, they will be routed to `'/users/signup'`. The browser knows this because it is listed as `post '/users/signup'`. 

Another new thing I learned is how to create an encrypted password in Sinatra. In the `gemfile`, install the gem `bcrypt`. Then in the `user table`, create a column with `:password_digest`. Next, in the `user_controller`, make sure you have the correct user selected by checking the `params[:username]` and then make sure to `@user.authenticate(params[:password])`. This makes sure the password belongs to the correct user and is encrypted when stored so it cannot be hacked.

Throughout my code, you will see that almost every `get` and `post` start off with 
> if is_logged_in? && current_user
>             session[:user_id] = current_user.id
>             erb :"url_here"
>         else
>             erb :"users/error"
>         end
				
The reason for this is to prevent someone else accessing a different account. `is_logged_in?` is checking if the user has a session id and `current_user` checks to make sure they are using their current session's id (since a session id changes every time they log out). Once it knows they are the current user, then it can create a new session id for the current user. 

When is `:id` used in the get or post request? This concept caused me a lot of errors, but now I feel like I've reached a greater understanding. The id is only needed in the url if it needs to be specific to the user or item. For example, if the user wants to create a new item, they wouldn't need a specific :id, they could go to `'items/new'`. However, if the user wants a specific item to be edited, they would need to have id in the url so the computer would know which item to go to. Additionally, a patch and delete would also need to be specific, otherwise all their items would be deleted. The reason `view` doesn't need its own :id is because the `get` request makes sure it is the current user before displaying their information. 


I hope you found this information helpful. Happy coding!
