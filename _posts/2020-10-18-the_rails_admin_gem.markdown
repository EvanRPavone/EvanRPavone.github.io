---
layout: post
title:      "The rails_admin gem"
date:       2020-10-18 15:52:23 +0000
permalink:  the_rails_admin_gem
---


For my Rails project I created a website that a uer can create an account and plan a trip for Strong Missions. The user can edit their profile, update a trip they have created or destroy it. The user can only see their own planned trips, but the Admin can see everyones planned trip in the Admin Panel.

Admin Panel? That is where the 'rails_admin' gem comes into play. This gem also uses the 'cancancan' gem which a very important gem because it is how you create and add roles to a user profile. On top of that, you will have to have the 'devise' gem already setup with a user table, models, and views. Once you have these gems installed, you can start creating your roles. This can get a little tricky so if you need a lot more guidance on the whole process you can check out this blog here: [Rails 6 (and 5): User Accounts with 3 types of Roles – Devise, Rails Admin, CanCanCan](https://altalogy.com/blog/rails-6-user-accounts-with-3-types-of-roles/). I am also using bootstrap to give the pages a more slick look. Before we begin with the adding the roles make sure you have authentication in your application controller:

```
class ApplicationController < ActionController::Base
    protect_from_forgery with: :exception

    before_action :authenticate_user!

end
```

The before_action above authenticates all users before every action in all of your contollers. Next is to add a skip_before_action to your home controller

`skip_before_action :authenticate_user!, :only => [:index]`

This will let you see your index page without having to login. Going to another page will make you login. Let's go ahead and setup the navigation bar so we dont have to worry about it later:
```
<li class="nav-item">
	<%= link_to 'About Us', home_about_path, class:'nav-link' %>
</li>

<% if current_user.nil? %>
<li class="nav-item">
	<%= link_to 'Log In', new_user_session_path, class: 'nav-link' %>
</li>
<li class="nav-item">
	<%= link_to 'Sign Up', new_user_registration_path, class: 'nav-link' %>
<% else %>
<li class="nav-item">
	<%= link_to 'Edit Profile', edit_user_registration_path, class:'nav-link'%>
</li>
<li class="nav-item">
	<%= link_to 'Log Out', destroy_user_session_path, method: :delete, class: 'nav-link'%>
</li>
<% end %>
```
If the user is signed in, then it will show edit profile and logout. If the user is not logged in then it will only show Login and Signup. Anything outside of the if and else statements will show no matter what, like the About Us page.

After you have your devise views and devise controllers generated make sure you update your routes.rb:
```
devise_for :users, controllers: {
    sessions: 'users/sessions',
    passwords: 'users/passwords',
    registrations: 'users/registrations'
}
```
Add  the rails_admin gem if you haven't done so and run bundle install then,
`rails g rails_admin:install` in your terminal. This will give you access to the Rails admin panel with` /admin` at the end of localhost:3000.

Navigate to config/initializers/rails_admin.rb to be able to use devise for your authentication and add:
```
  config.authenticate_with do
    warden.authenticate! scope: :user
  end
  config.current_user_method(&:current_user)
```
This is probably already in the file, you will just have to uncomment it.

Now it's time to get into cancancan, this is where you might run into errors, I sure did.

Make sure cancancan is in your gemfile and it is installed. Put `rails g cancan:ability` to generate your ability.rb model. Next you have to add your roles in a migration:
`rails generate migration add_roles_to_users superadmin_role:boolean supervisor_role:boolean user_role:boolean`
Before running db:migrate, you have to edit the table:
```
class AddRolesToUsers < ActiveRecord::Migration[5.2]
  def change
    add_column :users, :superadmin_role, :boolean, default: false
    add_column :users, :supervisor_role, :boolean, default: false
    add_column :users, :user_role, :boolean, default: true
  end
end
```
You can name your admin roles to whatever you want and then run `rake db:migrate`.
Congrats! You added roles, now you just have to do a bunch of other stuff. Hang in there!

Going back to your navigation bar, remember that if statement for can?, now its time to set that up. Navigate to `app/models/ability.rb` and edit the file to look like this:

```
class Ability
  include CanCan::Ability

  def initialize(user)
    # Define abilities for the passed in user here. For example:

    user ||= User.new # guest user (not logged in)
    if user.superadmin_role?
      can :manage, :all
    end
    if user.supervisor_role?
      can :manage, User
    end

  end
end
```
Edit the file to have the names of your admin roles. Now go to `config/initializers/rails_admin.rb`  and uncomment the CanCanCan section, if you are following along on the more indepth instructions there is suppose to be another can instead of cancan.
```
  ## == CancanCan ==
  config.authorize_with :cancancan
```
Go back to `app/model/ability.rb` and edit the code you added above to this:
```
user ||= User.new # guest user (not logged in)
can :manage, :all <------- Remove this once you have given your user permission to superadmin
if user.superadmin_role?
      can :manage, :all
      can :access, :rails_admin       # only allow admin users to access Rails Admin
      can :manage, :dashboard         # allow access to dashboard
end
if user.supervisor_role?
      can :manage, User
end
```
If everything is added properly, errors will most likely happen but it should work. Run your server and see if admin panel shows up in your nav bar. Click it and login/signup. Next is too add your admin role to the login you just created. Navigate to the admin panel and you will see a Users section the main section of the page, click it. Now find the user you created and on the right side there is a little edit button, click that. Scroll down, if needed, and check the box superadmin role and SAVE YOUR CHANGES! Congrats you have hopefully successfully added an admin panel.

This was a lot of fun to do, the errors I get are probably on my side but once you get it working it's so smooth and it helps out a lot if you are making a post, forum, or anything like that because you can control what content is being shown on your pages.

I hope this worked for you! Enjoy!








