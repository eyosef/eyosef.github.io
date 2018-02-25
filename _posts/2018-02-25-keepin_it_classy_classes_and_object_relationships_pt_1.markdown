---
layout: post
title:      "Keepin' it Classy: Classes and Object Relationships (Pt. 1)"
date:       2018-02-25 18:22:19 -0500
permalink:  keepin_it_classy_classes_and_object_relationships_pt_1
---


**I**n the course of my studies with Flatiron, I have had to shift the paradigm of my thinking. I've become more patient and accepting of programming as a process. It's all about the journey *and* the destination. Debugging is a central pillar to programming. I've learned to read errors closely, debug systematically, and think through the logic of my code to ensure it's effective.

<br>
![](https://studentaffairscollective.org/wp-content/uploads/2014/09/keep-calm-and-program-on-5-257x300.png)</br>

There were some challenging concepts that crossed my path, but none were as challenging as classes and object relationships. Even though these are challenging concepts, they're useful and efficient for things like data management. **So let's dive in and explore! We'll focus on setting up a basic programmatic framework for our classes. (The next blog post dives into object relationships)**

### Scenario:

You work for a company that coordinates group travel experiences. Your employer needs you to keep track of global tourism trends on countries being visited, lodging and traveller demographics. This data will have a tremendous influence on your employer's marketing campaign. 
<br>**How do we use classes and object relationships to track this data?**</br>

* *First thing's first:* What are the goals of your code? In this scenario, you need to keep track of vacation spots, hotels and traveller information. 

* *Then:* What are the methods or classes needed to accomplish this? Think about the relationships between what you're tracking. Vacation spots have many hotels and many visitors (or travellers). One hotel can have many travellers but only one destination. (We are excluding global hotel chains). Travellers can have many hotels and many destinations over a period of time. It sounds like we'll need 3 classes;

```
class Destination 
end 

class Hotel
end 

class Traveller 
end 
```


* *Finally:* What `attr_accessor`(s) are needed in each class to collect data and establish object relationships? Let's approach this one class at a time. Vacations spots will have many hotels and many travellers, but let's start small and keep it simple. It's better to have a gradual approach than to try to accomplish everything at once. 

![](http://www.nb-coaching.com/v2/wp-content/uploads/2014/08/think-big-start-small-300x224.jpg)
 
 
In order to collect data on vacation spots, our `attr_accessor` will need `:country`. It will look like this;

```
class Destination

    attr_accessor :country 

end
```

If we'd like to set variables and pull variables, `attr_accessor:` is the approach to use. (Fun fact: `attr_reader` can be used to set a variable once and never change it!) In order to initialize objects, we'll need the method `#initialize`. 

```
class Destination 

    attr_accessor :country 

    def initialize(country)
    @country = country
    end

end 
```

Now that we can initialize an object, how do we `return` all instances of our objects? This is a simple, but multi-step process. In order to `return` instances of a country, we need to **(#1)** create an empty array outside of `#initialize`. This array must be set equal to a class variable to expand it's scope and allow it to be called on in the different class methods. (This is relevant to step 3). Then, inside of `#initialize`, we can **(#2)** push all instances of `country` inside of the array.

Let's take a look at steps 1 and 2 below;

```
class Destination

    attr_accessor :country 

    @@destinations = []

    def initialize(country)
    @country = country
    @@destinations << self
    end

end
```

(Fun fact: If we wanted each instance of `country` to have an empty array, we would include an instance variable inside of `#initialize`. This would be helpful if we anticipated that one instance would have many objects. For example, we could have an empty array inside of each instance of `country` to keep track of the cities. Kind of like this; `@cities = []`)

Finally, we can **(#3)** `return` the array in a class method, `.all_destinations`.

```
class Destination

    attr_accessor :country 

    @@destinations = []

    def initialize(country)
    @country = country
    @@destinations << self
    end

    def self.all_destinations
    @@destinations
    end

end
```

This way, we can do this;

```
france = Destination.new("France")
france  #=> #<Destination:0x0000000004ece560 @country="France">

Destination.all_destinations  #=> [#<Destination:0x0000000004dff0f8 @country="France">]

```


![](https://thumbs.dreamstime.com/t/woman-climbing-mountain-holding-ladder-to-get-red-flag-top-background-blue-sky-vector-flat-design-67928537.jpg)

Now that the basic framework of Destinations  has been established, let's implement the same code for our Hotel and Traveller class. This will ensure we can initialize instances of Hotel and Traveller, respectively. This will also ensure we can `return` all instances of Hotel and Traveller, respectively.

```
class Hotel

    attr_accessor :hotel

		@@all_hotels = []

    def initialize(hotel)
      @hotel = hotel
      @@all_hotels << self
    end
		
		def self.all_hotels
		@@all_hotels
		end

end



class Traveller

    attr_accessor :name

    @@all_travellers = []

    def initialize(name)
    @name = name
    @@all_travellers << self
    end 

    def self.all_travellers
    @@all_travellers
    end

end
```

Feel free to play around with the code above, using online IDEs like [repl.it](https://repl.it/repls). It's a great opportunity to practice instantiating objects and calling on class methods. The next blog post will explore how to establish object relationships that ensure our classes interact with each other.









