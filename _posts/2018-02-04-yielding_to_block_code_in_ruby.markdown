---
layout: post
title:      "Yielding to Block Code in Ruby"
date:       2018-02-04 23:57:18 -0500
permalink:  yielding_to_block_code_in_ruby
---


**Y**ield keyword is difficult for the novice programmer to understand. When building simpler code, alternative methods like `#each` or `#map` are more appealing because they're easy to read. Nonetheless, `yield` is a powerful tool that is important to understand as your code becomes more and more complex. 



To help understand `yield`, let's imagine you're driving on a one-way street towards a traffic circle. You pull up to the traffic circle, and follow the `yield` street sign by stopping and allowing the cars in the traffic circle to pass. Then, when it's all good (so to speak), you continue driving.



That's essentially what `yield` does in a method. The method begins to implement it's code, pauses to invoke code in `yield`, and then continues to implement the rest of the code in the method. In many ways, `yield` kind of operates as traffic control for complex programming.



![](https://3h308wkqnxzfmr3r2xse3b16-wpengine.netdna-ssl.com/wp-content/uploads/2016/05/giphy-4-3.gif)



It's kind of like driving a car - traffic circles are useless until there's traffic. `Yield` is most useful as your code gets jammed with complexity. **Let's take a look at an example;**



#### Scenario:


You're a web developer for a newly-opened hotel. The owner needs you to send a greeting to guests that have checked in. Every time a guest checks in, the owner wants an updated list of guests that received a greeting. (He takes customer service very seriously). How does `yield` come into play?



```
def greet

guests = ["Amy", "Kevin", "Alice", "Arthur"]

guests.each_with_index do |guest, index| 
  puts "Welcome to Hotel Sunrise, #{guest}!" 
  yield(guest)
  puts "You are guest number #{index+1}."
  end 
end 

greeted_guests = []
guests = ["Amy", "Kevin", "Alice", "Arthur"]

greet { |guest| greeted_guests << "#{guest}" }
```


#### Notes on the Code;

* **First**, notice how the `.each_with_index` iterator allows us to iterate through the first element of `guests` array, putsing `"Welcome to Hotel Sunrise, #{guest}!" ` 

* Immediately after this line of code is executed, all invocations that follow #greet stop. 

* The keyword `yield` invokes block code outside of #greet. The block code that's invoked is `greet { |guest| greeted_guests << "#{guest}" }`. In this example, the interpolated`#{guest}` is pushed into the array `greeted_guests`. 

* Since the block code has been executed, #greet is re-invoked, putsing `"You are guest number #{index}."`.

* Congratulations! The first iteration of guests array has been completed. This means #greet has putsing;
                    Welcome to Hotel Sunrise, Amy!
                    You are guest number 1.

* But also: Congratulations! The block code pushed Amy's name into the array, greeted_guests. Not only has Amy been greeted, but we have an array that's keeping track of this. This means that every time a guest is greeted, our code automatically updates the array to ensure we have an instantaneous record of who has been greeted.

**W**hen I think about web development, it largely involves working with pre-existing code, as opposed to creating original code. `Yield` is a really helpful keyword to dive into your code and really get a jumpstart on making changes.




