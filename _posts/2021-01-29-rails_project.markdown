---
layout: post
title:      "Rails Project"
date:       2021-01-29 17:38:57 +0000
permalink:  rails_project
---


I made an application called Sneak A Head where users can view upcoming sneaker releases to get the chance to enter a raffle to purchase the shoes.  My thought process while creating this project started on a piece of paper.  Explaining the details of my project, telling the story of my application, and jotting down the associations.  I must admit drafting out my project on paper got super messy, really quick so I moved to draw.io to organize my associations and to help visualize them.   This is where it got super complicated.  Associations was one of my struggles.  I couldn't figure out the relationships in correct way and got everything sort of mixed up.  My models are User, Raffle, and Shoe.  I originally had an additional model Entry however, I left that out.  Here is a quick snippet of my draw.io that I originally had drafted out: ![](https://imgur.com/FOQlHbs)

Here is where my everything started to get tricky.  As you can see I started adding in the attributes and that empy square was going to be a fourth model. Yikes! So here is the scaled down version.  This helped get the basic of the app get started and get it going. ![](https://imgur.com/lkAHDTv)


After I got my controllers, models generated and schema migrated.  To get my app to show any data I had to seed some data, so I thought it will be great idea to scrape. To scrape I decided to use the nokogiri gem. Let me say this,"Do not spend your entire project scraping like I did!" While I was scraping the data that I needed, it was much more difficult adding the data and seeding it to your project.  After spending days trying to scrape and input that data in the database, after watching countless tutorials, google resources, and help from my instructor, I decide to just write seed data. Once I seeded my database I quickly got my login page working and ominauth with facebook running properly.  

This project wasn't my strongest and working on better ways to make my project better.  I next goal is to work on understanding the concept better and getting the logic of my applications stronger.  Rails is magic however, while it's magic it will have you a bit confused really fast.  
