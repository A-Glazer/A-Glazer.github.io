---
layout: post
title:      "Sessions vs Params"
date:       2019-05-15 17:57:29 +0000
permalink:  sessions_vs_params
---


Are you getting confused between params and sessions? Well here is the difference. 

# What is a param?
A param stands for parameter. It is used when you want to take the user's information and turn it into a url. For example, if you would like to convert the username into a url, you would do params[:username]. 

## What is a session?
A session is a hash that keeps track of the user's activity during the duration of time that they are logged in. 

## So when do you use param vs session?
When a person signs up to a website, their information is saved to a database. The next time they log in, the program needs to check if their information already exists. To access it, they would compare using params, does the username given match the params[:username]? 
Once the user is logged in, a session is created. So now if you want to find out something about them, you would check their session[:id] rather than params. After they log out, that session is no longer active and cannot be referenced in connection with the user.


**Here is an example of params vs. sessions:**

```
     1. post '/login' do
     2. @user = User.find_by(:username => params[:username])
     3. if @user != nil && @user.password == params[:password]    
     4. session[:user_id] = @user.id```
			
In this example, `line 2` is checking if the `@user` that was submitted matches with a `params[:username]` that is already in the database. `Line 3` is checking to make sure the user information is not nil and the password matches, again using `params`, then `line 4` make a new `session` using the `user_id` that was submitted. 
