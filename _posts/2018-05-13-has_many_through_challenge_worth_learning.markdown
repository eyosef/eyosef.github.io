---
layout: post
title:      "has_many_through: :challenge_worth_learning"
date:       2018-05-13 21:18:37 -0400
permalink:  has_many_through_challenge_worth_learning
---


**H**as many through gave me a taste of how complicated an app can become through its associations. There's a certain irony to learning programming, and it certainly didn't escape me. Here I was, learning about Rails associations through a dynamic website that likely uses dozens of associations to facilitate my education. But that's what makes programming exciting! Someday soon, I'll be using these associations to make the world a better place, one UX at a time.

In order to understand `has_many_through`, let's imagine you and a few colleagues are at the edge of a cliff, staring across a canyon. On the other side of the canyon are more of your colleagues. You have to ask them a question, but can't access them directly. Since there is no bridge, and you have no carpentry skills, you do what most people would: you make a paper airplane. Then, you write down your request (maybe a question), and send the paper plane across the canyon, to your colleague. When your colleague receives the paper airplane, they send it back with info that satisfies your question.

![](https://media.giphy.com/media/uI5Gr6lTymcoM/giphy.gif)

`has_many_through` is the paper airplane. It operates as a go-between for two datasets that need to access information indirectly.

#### Scenario:

You're a web developer for a bike-shop that needs an app for its customers. What kinds of associations could require `has_many_through`? 

```


class BikeShop 
   has_many :bikesales
   has_many :customers, through :bikesales
end


class Customer 
   has_many :bikesales
	 has_many :bikeshops, through: bikesales
end


class BikeSale
  belongs_to :customer
  belongs_to :bikeshop
end
```

![](https://media.giphy.com/media/l3vRfzIm6BOdyPsM8/giphy.gif)

#### Let's think about this:

Just imagine a cyclist (without a bike) at the edge of one cliff. Across the canyon is a bike shop at the edge of another cliff. Bike sales (a.k.a. receipts) operate as a go-between. In order for a bike shop to access data about their customers, the bike shop needs to examine their bike sales. in order for a customer to access data about their bike shop, they need to examine their bike sales (or from the customer's perspective, their bike purchases).

This is why BikeSale is considered a join table - because it establishes an ActiveRecord association. Data kept in the bike_sale table could include;
   * t.string :bike_type
   * t.integer :bike_cost
   * t.integer :bike_shop_id
   * t.integer :customer_id 

This table would not only contain information on the product sold, but the customer and shop involved. See why it's a join table?

**T**his association has a ripple effect into our controllers. If we set `@bikeshop` equal to the appropriate `params`, than `@bikeshop.bikesales` could be iterated on to access products and customers. We could access this information in the Controller to display it in our View. All of the information relevant to a single purchase can be accessed in one page. Convenient and effective.

