---
layout: post
title:      "Sinatra Project "
date:       2020-06-05 02:39:28 +0000
permalink:  sinatra_project
---


I want to share my thought process around creating and building this project and share the areas of struggle and what I learned throughout the process.   In my opinion, learning Sinatra was very straightforward but also dynamic.  


The application I created is called Discuss Plus, a message board where user can create, edit, delete and view their own posts and other users content or a post.  My stretch goal was to have users reply to other users posts however, I didn't create that part yet but will continue to add that feature as I go along in the cohort. 

# App Requirements
I created two models a User and PostDiscussion model.  A User has many post discussions and a post discussion belongs to a user.  In which both models inherit from ActiveRecord::Base. 

**A user should be able to:**
1. Sign-up for a new account
2. Log-in and Log-out to the account
3. Update her account information and password
4. View their posts and other users posts
5. Create, edit, and delete their posts

**Post Discussions has a topic, content and date that the user published the post.**  

I have 3 controllers: Application, Posts and Users controller. 
1. Application Controller: which inherits from Sinatra Base, configures the sessions controllers and this is where I stored my helper methods.  
2. Posts Controller: this controller inherits from ApplicationController, and defines RESTFUL route actions relevant to a Post.
3. Users Controller: this controller inherits from ApplicationController, and defines RESTFUL route actions relevant to a User.

All three controllers I mounted in the config.ru file which I mounted the Application Controller by using the run command and Posts and Users Controller inherits from Application Controller by using the command use.  


**Creating and Migrating my tables**

I created and migrated my tables by using rack db:migrate.  My users and post_discussion table inherits from ActiveRecord::Migration which allows you easily write migrations and make changes to your tables in a Ruby DSL instead of SQL.    I also created seed data to test that data in tux just to make sure my tables are set up correctly. 

```
class CreateUsersTable < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name 
      t.string :email
      t.string :password_digest

      t.timestamps null: false
    end
  end
end



class CreatePostDiscussions < ActiveRecord::Migration
  def change 
    create_table :post_discussions do |t|
      t.string :topic
      t.string :content
      t.string :date
      t.integer :user_id
      
      t.timestamps null: false 
    end
  end
end
```

Finally, after I migrated the tables,and the models were created, it was time to start building my app.  I got a late start when starting this project. I wanted to make sure that I was fully understanding the basics of Sinatra, how the MVC interacts and understand the concepts of Restful routes.  During that time, I still struggled grasping the concepts so it took me 2 weeks to complete this project. It was alot of moving pieces that I couldn't figure out.  My major stuggle was the validations and authentication so, let's discuss that.  A user has to have it's own unique data.  Unique data such as name, password, email. This data is used when the user has to log-in and sign up to the app.  Validations are used to ensure that the users unique data is valid and that users data is secured and belongs to that user.  The important data that is secured is the password.  The password is secured by a gem called b-crypt, which encrypts the password into a hashing algorithm.  This hashed version of our users' passwords is put in our database in a column called password_digest which is in the sample code above in the CreateUsersTable.  Next, I used a macro called, has_secure-password that works with the gem b-crypt which is placed in my User model.  This will not allow the password to be stored in the database in plain text.  

```
class User < ActiveRecord::Base 
  has_secure_password
  validates :email, :password, presence: true  
  has_many :post_discussions
end
```

The activerecord macro validates :email, :password, presence: true is an activerecord validation which means that any instance from the User class is not valid without an email and password when persisting data into the database.  Therefore, we can not authenticate the user to log in or sign up.  I then created the helper methods to help validate if the user was logged in and if the user is currently using the app or not. 



**Restful Routes**

I used restful routes for the users controller and post discussions controller.

I did have slight struggles with the patch route, the update action.  Where it modifies an existing post based on ID in the url.  I created several helper methods to help set validations to that the user can edit it's own post.  


```
patch '/posts/:id' do  #action handles the edit form submission
     set_post
    if logged_in? && if authorized_to_edit?(@post)
        @post.update(topic: params[:topic], content: params[:content], date: params[:date])  
        redirect "/posts/#{@post.id}"
       else
        redirect "users/#{current_user.id}"
       end
       redirect '/'
       end
   end
```

This project was challenging for me however, I'm so happy to be more confident in how Sinatra works and how to use sinatra and activerecord to build dynamic web applications.  
