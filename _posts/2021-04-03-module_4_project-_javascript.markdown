---
layout: post
title:      "Module 4 Project- JavaScript"
date:       2021-04-03 13:32:56 -0400
permalink:  module_4_project-_javascript
---


The JavaScript module is packed full of new concepts, different syntax and the code flow is different from Ruby.  My project is called Kitchen Alchemist.  Where users can select a food item found in the kitchen and create different recipes that benefit the skin and hair.  I came up with this idea because I enjoy DIY’s and wanted to create an app where people can share the DIY recipes.  The planning of my application went smoothly until it was time to execute.  

First challenge was where to start. I had to review many project review videos just to get my project started.  The first step was creating my frontend and backend repositories and then to connect my backend with my front end.  

I first created  my app: 

```
rails new <my_app_name> --database=postgresql --api


```


For my app I have two models: 

```
class Item < ApplicationRecord
    has_many :recipes
end

class Recipe < ApplicationRecord
    belongs_to :item, optional: true
end		

```

Schema: 

```

ActiveRecord::Schema.define(version: 2021_03_13_041910) do


  create_table "items", force: :cascade do |t|
    t.string "name"
    t.string "benefits"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

  create_table "recipes", force: :cascade do |t|
    t.string "title"
    t.string "ingredients"
    t.string "instructions"
    t.integer "item_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

end

```

Once I created my schema and seeded my data, I created my controllers and then created my routes.  I set up the routes as follows, using namespacing to organize the controllers and allow for version control:


```
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :items, only: [:index, :show]
      resources :recipes, only: [:index, :create, :destroy, :show]
    end
  end
end


```

I decided to do namespacing because I learned this in module 3 and wanted to try it in my project for the first time. To read more about naame spacing please read here: https://learn.co/lessons/namespaced-routes-reading

Once I created my database, controllers and routes.  I was ready to create my front end. I used Fast JSON API to serialize my data. Just incase you do not know what serialization is, it means to convert an object into that string and Fast JSON API is a gem that does the Json conversion for you.  Here is an example of the serialization code: 

```
class ItemSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name, :benefits
  
end


class RecipeSerializer
  include FastJsonapi::ObjectSerializer
  attributes :id, :title, :ingredients, :instructions, :item_id, :item
  
end

```

To connect my backend with the frontend and to make my first fetch request I had to add a gem CORS.  CORS means cross orgin reference sharing. CORS is a security feature that prevents API calls from unknown origins.  In order for me to make a fetch request to my domain  http://localhost:3000/api/v1/recipes I added the gem 'rack-cors' to my gemfile and updated some information in my configuration file to allow the domain. 


I would love to write a full blog about my entire process but I rather share the challenges I faced.  The major challenge  was merging my model attributes together through the front end.  To elaborate more,  I struggled with associating my models and displaying them to the front end and manipulating the DOM to display what the user inputted in the form.  Also, I wanted to add more funtionality and create the app as I envisoned during my planning phase. Furthermore, I struggled with organizing my code and understanding why the functions I created was not displaying the data. That mostly due to scoping. 


This project definitely was not my best project and I definitely plan on learning more about JavaScript and prefecting this project as well creating several more.  I hope this project prepared me for the final module before graduation.  I look forward to learn more, create more and continue to love programming. 








