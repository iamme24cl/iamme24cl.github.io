---
layout: post
title:      "MeroWineNotes - a simple Sinatra App"
date:       2020-12-24 21:54:34 -0500
permalink:  merowinenotes_-_a_simple_sinatra_app
---

This is an app that lets you take notes of your favorite wines. When I was working as a sommelier, I was constantly tasting new wines and taking notes on them. So, I built something that can be used to take notes on wines, in a pattern that sommeliers, or individuals in similar fields, generally use. 

The goal with this app was to build something that can be used to create new instances of the user's favorite wines giving them attributes like producer name, grape varietal, vintage, tasting notes etc. The user should be able to save their wines in a database, update/make changes to them, and delete them. The app should also have an authentication system allowing users to log in, log out and only make changes to their own wines or their own account.

This is a  Sinatra based app that uses a MVC(Model, Views and Controller) paradigm. I used ActiveRecord for the database. All my models inherit from `ActiveRecord::Base` giving them access to  ActiveRecord Association methods like `has_many` and `belongs_to` along with input validations for form input from users. For authentication, I used the ruby gem `BCrypt` to encrypt the passwords. BCrypt will store a salted, hashed version of our users' passwords in our database in a column called `password_digest`. Essentially, once a password is salted and hashed, it is extremely difficult for anyone to decode it. This gem can be used with the ActiveRecord macro `has_secure_password`  which gives us all of those abilities in a secure way that doesn't actually store the plain text password in the database.

```
# add gem 'bcrypt` to gemfile

class User < ActiveRecord::Base
  has_secure_password
end
```

The ActiveRecord macro `has_secure_password` gives us access to methods like `.save` and `.authenticate` . Because our user has `has_secure_password`, we won't be able to save this to the database unless our user filled out the password field. Calling `user.save` will return false if the user can't be persisted.
To check the password, we use the `.auhenticate` method on our User model. This will check if that user's password matches up with the value in password_digest.

Then I used Rakefile to help with migration tasks using:  
```
ENV["SINATRA_ENV"] ||= "development"
require 'sinatra/activerecord/rake'
```
This was very helpful as you just run a few simple rake commands such as `rake db:migrate` and wallah! you have all your migrations and `shcema.rb` file all created for you.

In my ApplicationController, I set my views, public folder, enabled my sessions, and set a session_secret. 
Here, I also defined some helper methods to help with the authentication and login. Along with `logged_in?` and `current_user`, I also used a `authentication_required` method to help with not having to use conditional statements in every controller action requiring authentication:
```
def authentication_required
 if !logged_in? 
  flash[:error] = "You must be logged in"
  redirect "/login"
 end
end
```


To use the app, clone it from this repo: https://github.com/iamme24cl/mero-winenotes . Then cd into **mero-winenotes** , run **bundle install** to install all dependencies, and then run **shotgun**.

Shotgun is a small Ruby gem that makes it easier to develop and test Rack-based Ruby web applications locally by starting Rack with automatic code reloading.
You should see something like this:
```
== Shotgun/WEBrick on http://127.0.0.1:9393/                                      
[2020-12-24 17:37:33] INFO  WEBrick 1.4.2                                         
[2020-12-24 17:37:33] INFO  ruby 2.6.1 (2019-01-30) [x86_64-linux]                
[2020-12-24 17:37:33] INFO  WEBrick::HTTPServer#start: pid=138 port=9393  
```
The application is now loaded and being served from port **9393**, the default shotgun port. The application will respond to requests at `http://127.0.0.1:9393` or, more commonly, `localhost:9393`. Go ahead and visit `localhost:9393` in the browser. 

Here you can register for a new account or log in after you create an account. This is the `get "/"` route and the homepage of the application. When you click on **Log In**, this will send a get request to `'/login'` which renders the log in form. The log in form submission will then send a post request to `'/login'. During this request, we find the user using `params[:email]`, and then we authenticate the user using the `.authenticate` method provided my ActiveRecord.  If the password provided by the user in the params, matches the one on file in the `password_digest` column in our database, the user is successfully logged in by assigning the `user_id` to `session[:user_id]` .  

After logging in, you will be redirected to "/wines". During this `get` request, an instance variable `@wines` is assigned all the wines that belongs to the current user. This instance variable can then be used to display all the wines via the wines index page `erb :"/wines/index.html"`.

When logged in, you will able to view other member's wines and profile, but you can only create, update, and delete your own account/wines, and not others. The links to all these options will be at the top navigation portion of the page.

The **My Profile** link will send a get request to `"/users/user.id"` and render the users invidual show page/profile page. Here, I used a conditonal statement to render 'user edit' and 'user delete' buttons/links if the user viewing the page is the current user, otherwise, all the wines belonging to the user selected is displayed.

The **Add New Wine** link will send a get request to `"/wines/new"` . This requests calls the `authentication_required` method and checks if the user is logged in before rendering the form to create a new wine. After the user submits the filled out form, this will send a post request to `"/wines"`. During this request, a new instance of the wine is created using the params from user input, the new wine is assigned to the current user, and saved in the database.  This process will also trigger input validation provided by ActiveRecord when calling the `.save` method while creating the new wine. If the input provided by the user, meets all validations defined by us, the new wine will be saved and the user will be directed to the new wine show page, otherwise an error message describing the error is displayed and the user is redirected to the form page to create a new wine.

The **Members** link will send a get request to `"/users"`. This will render the `"/users/index.html"` page. Here you will find links to all the current members. You are able to see other members' wines and profile information but not able to edit or delete them.

Lastly, the **Logout** link as the name itself says, will log you out of the application by clearing the current session. You will then be redirected to the home page.

```
get '/logout' do
 session.clear
 redirect '/'
end
```

Thank you for reading my blog and taking the time to checkout out my app. I hope you were able to get something useful out of it.



































