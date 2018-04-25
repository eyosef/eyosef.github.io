---
layout: post
title:      "Combining Passion and Programming: My Sinatra Project"
date:       2018-04-25 14:13:41 +0000
permalink:  combining_passion_and_programming_my_sinatra_project
---


**I** have to say, completing this project was surprisingly fun. It didn't occur to me how much I had absorbed during the last 3 months. Completing this project was like riding a bike. It was a tad challenging to get started, but once I did, I couldn't stop.

<iframe src="https://giphy.com/embed/26tn0ONYXTynFU3Be" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/woman-bike-ameliagiller-26tn0ONYXTynFU3Be">via GIPHY</a></p>

Prior to starting the lab, I researched different ruby gems that build out file trees. It turns out a Flatiron alum created this [gem](https://github.com/thebrianemory/corneal) for sinatra/activerecord. Sweet! Once I installed the gem, it was time to decide what to do.

As an avid gardener, I decided to create a gardening app that would store plant varieties. Users could access the database, as well as contribute to it. Thus, 'Green Thumb Fun' was born.

## Project Management: Planning Your Web App

 The next step involved planning what my app would look like. [Draw.io ](https://www.draw.io/) is a great tool for web developers. It's visual, but simple. I used it to outline my goals for the database and user experience. In order to have a functioning, effective app, I needed at least two tables; a plant table and a user table.
 
 
 ```
1.  User table
      - has many plants
      - Columns: username, password_digest & email
      
2.  Plant table
      - belongs to a user
      - Columns: variety, growth type, days (number of days plants needs to grow before transplanting), details, & user id
 
 ```

<iframe src="https://giphy.com/embed/O9iBAA1CsA27C" width="480" height="291" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/cinemagraph-fixie-O9iBAA1CsA27C">via GIPHY</a></p>

 But that wasn't enough; I needed to outline my expectations of the app's functionality, which I did through draw.io. The user needed to be able to create an account, log-in, log-out, edit their account information, submit a plant variety to the database, edit their submissions and delete their submissions.
 
 I also decided that every user would have a Profile Page. This page would provide their account information (email address and username) as well as their submissions. I figured it would be really interesting if upon immediately logging in, a user would be directed to their profile page. Since their profile contains information related to the user, they could review, edit or delete submissions.
 
 As if that wasn't enough, I also needed to think about the functionality of the different webpages. It was really exciting for me because as a gardener, it was easy to come up with practical, but creative features that would facilitate the gardening process.
 
 ## Seeding the Database through Dynamic Webscraping
 
 In order to have accurate information seeded into my Plant database, I decided to web scrape a public resource. Usually, I seed a database using `.create` and `rake db:seed`. Both approaches are perfectly fine, but I wanted to see how web scraping could be applied in Sinatra and ActiveRecord. Webscraping took a few days of coding, testing and debugging, but it worked! I was able to seed and migrate my database with approximately 135 plant varieties. It was definitely a proud moment.
 
 <iframe src="https://giphy.com/embed/4ZrTDnFt1V3ohpURPH" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/electriccyclery-india-cycling-4ZrTDnFt1V3ohpURPH">via GIPHY</a></p>
 
 All in all, it was really interesting to think about how database management coincides with the user experience. The information we use to create accounts, or create submissions could end up stored in a database to be accessed for future use by the User. Talk about interesting! Whether it was Facebook or Github, I have always contributed to these kinds of databases as a user. Now, I contributed as a programming and it felt great. People can connect and stay connected through these kinds of technological capabilities.
 

 
 
