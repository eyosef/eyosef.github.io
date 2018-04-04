---
layout: post
title:      "Keepin' it Classy: Classes and Object Relationships (Pt. 2)"
date:       2018-04-04 21:27:35 +0000
permalink:  keepin_it_classy_classes_and_object_relationships_pt_2
---


In part 1 of [Keepin' it Classy: Classes and Object Relationships](http://edensenait.com/keepin_it_classy_classes_and_object_relationships_pt_1), we created three classes; `.Hotel`, `.Destination` and `.Traveller`. Each class is equipped with `attr_accessor`, `#initialize` and a class variable set equal to an empty array, to capture all instances of `self`. Below is where we left off;

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

Now that we have our framework established, let's start establishing object relationships. so our classes can meaningfully interact with each other. Destinations have many hotels and many travellers. One hotel has many travellers but one destination. Travellers can have many hotels and many destinations over a period of time.


Let's start with our class of Destinations. How do we ensure `.Destinations` has many hotels? First, I updated my `attr_accessor` and `#initialize` to allow the option of instantiating a destination with a hotel. I also created `@@hotels = []` to store all instances of hotel, and did the same through `@@travellers`.

```
class Destination

    attr_accessor :country, :hotel

    @@destinations = []
		
		@@hotels = []
		
		@@travellers = []

    def initialize(country, hotel=nil)
    @country = country
		@hotel = hotel
    @@destinations << self
    end

    def self.all_destinations
    @@destinations
    end

end
```

Then I created the method `#add_hotels`. Each time we use this method, hotel becomes instantiated as a new instance of `.Hotel`, and pushed into the array of `@@hotels`. We can use class method `.all_hotels` to return


```
	def self.add_hotel(hotel)
    @@hotels << Hotel.new(hotel) unless @@hotels.include?(hotel)
  end
	
	def self.all_hotels 
	  @@hotels 
	end
```

Let's do the same thing, but with travellers. Let's make sure `.Destination` can also have many travellers.

```
	def self.add_traveller(traveller)
    @@travellers << Traveller.new(traveller) unless @@travellers.include?(traveller)
  end
	
	def self.all_travellers
	  @@travellers
	end
```

So let's use our code!

```
france = Destination.new("France", "Marriott")
Destination.add_hotel("Marriott")

brazil = Destination.new("Brazil", "Embassy Suites")
Destination.add_hotel("Embassy Suites")

eritrea = Destination.new("Eritrea", "Residence Inn")
Destination.add_hotel("Residence Inn")


print Destination.all_hotels 
    #=>[#<Hotel:0x0000000004dce908 @hotel="Marriott", @destination=nil>, #<Hotel:0x0000000004dcf308 @hotel="Embassy Suites", @destination=nil>, #<Hotel:0x0000000004dc3fa8 @hotel="Residence Inn", @destination=nil>]
```

It looks like our class `.Destination` has many hotels!


