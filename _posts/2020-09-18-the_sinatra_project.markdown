---
layout: post
title:      "The Sinatra Project"
date:       2020-09-18 10:04:07 -0400
permalink:  the_sinatra_project
---


I love it. Sinatra is a really fun time for me especially because it can use HTML and CSS, which is my favorite thing to do. My project allows users to write a review on video games they have played and post them to a game reviews page. On this page they are able to see other reviews by other users. The user will also have the ability to edit or delete their reviews. [Click Me](https://youtu.be/j-aPzFtImqg) to see my demo.

The user is able to create and account which adds their info to a database including a secure password using the bcrypt gem. When it comes to the user filling out their information on the signup page, it sets the key value for the params hash. For example in my code for my signup form:
```
<label for="username">Username:</label>
<input type="text" name="username" id="username" required>
<label for="password">Password:</label>
<input type="password" name="password" id="password" required>
```
the name attributes in my inputs define the keys in the params hash, and their associated values are the user inputs, so they can be used in my controller like so:
```
user = User.create(:username=>params[:username], :password=>params[:password])
```
the params would get sent to the controller from the browser and then the controller would send the username to the user variable. If I were to signup and put my username as EvanPavone and put in my password it would send the code below to my user variable:
```
user = {:username => "EvanPavone", :password => (encrypted password)}
```
```
params[:username] = "EvanPavone"
```

The users have many reviews and the reviews belong to the user. After I got the database setup it was smooth sailing from there. The issue I had an issue with was implementing the information onto the page. I kept getting errors because I didn't define my methods correctly, which was an easy fix, I just tend to overthink.

I know we weren't suppose to focus on the HTML and CSS side of things but I really wanted to and I think it turned out pretty well. Using sections really helps organize the page and is easy to edit the css for each section.


