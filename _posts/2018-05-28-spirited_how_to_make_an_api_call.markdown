---
layout: post
title:      "Spirited: How to make an API call"
date:       2018-05-28 15:33:35 -0400
permalink:  spirited_how_to_make_an_api_call
---


My rails app, Spirited, was a huge step for me. I had never made an API call, let alone created a rails app before, so this was unchartered territory. I was really excited about using an API, because APIs are part of the future of web development. They provide the tools and protocols necessary for a web developer to dive in, assemble and produce a great program for the user. It was hard, but I'm a fast learner and I was able to pick it up quickly. 

When I researched how to make an API call, I found it to be extremely confusing. So in the spirit of #payitforward, this blog examines how to make an API call.

One fundamental component of an API call is deciding what API to use. The quality of an API varies greatly, so it's important to do your research. Research common problems developers faced when using the API. Think about what you want to accomplish - does the API documentation have clear instructions? Is the API well maintained? What format does the API recommend using? XML or JSON? It's really important to invest time in researching and vetting your API. This is the difference between having a polished, clearly defined project versus having to scrap and restart your project several times.

Once this has been squared away, it's important to think about the kinds of tools that will facilitate your API call. 
These are gems I recommend learning about as you decide what tools to use; 

* `gem 'dotenv'`
* `gem 'figaro'`
* `gem 'pusher', '~> 1.3'`
* `gem 'jsonapi-resources'`

Next, request your access key. The process of doing this varies across APIs, but in general you should create an account and submit a form to request the access key. This shouldn't take more than 10 minutes. Research your API documentation to determine what the URL is, and what endpoints (the API's routes) you need to use to have a successful rails app.

Once you have the access key, it's important to store it so that no other user can access it. Inside of your `config` directory, create the file `application.yml`. This file will store your access key. As you can see, the variable can store the access key, API URL, and the endpoint. Your file should look like this;

```
stores_access_key = "https://lcboapi.com/stores?access_key=01234abcd"
```

Add your file to `.gitignore` - this way, when you push your app to Github, `application.yml` won't be available to the public. This protects your app from hackers. You `.gitignore` file should look like this;

```
/config/application.yml
``` 

Let's create a services directory inside of the app directory. Inside of the services directory, create a `.rb` file. Mine was `Api.rb`. Inside of this file, create the class of Api, with a method name of your choosing;

```
   class Api
	 
	 def stores 
	 end 
	 
	 end 

```

Inside of `#stores`, we'll make the API call;

```
   class Api
	 
	    def stores 
      stores = open(ENV['stores_access_key'])
      stores_data = JSON.parse(stores.read)
			end 
	 
	 end 

```

If you go into binding.pry, you'll see that `stores_data` returns a hash! Congratulations, you have made a successful API call!! 

At this point, use binding.pry to determine how you're going to iterate through the hash and persist the API data to your database. Ideally, you want to limit the amount of calls you make to the API. It takes more time/energy for your program to implement an API call as opposed to a database query.


 
