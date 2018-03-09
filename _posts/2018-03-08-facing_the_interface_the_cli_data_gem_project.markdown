---
layout: post
title:      "Facing the Interface: The CLI Data Gem Project"
date:       2018-03-09 01:41:13 +0000
permalink:  facing_the_interface_the_cli_data_gem_project
---


**W**hen I first started this lab, I was extremely nervous. I thought back to when I was a child, and I placed magnets on the family desktop computer because it looked cute. It *was* cute. Then the computer crashed. It wasn't so cute after that. It's irrational, but on some level I was afraid the equivalent would take place in this lab. 

<iframe src="https://giphy.com/embed/KupdfnqWwV7J6" width="480" height="373" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/michael-jackson-popcornjackson-KupdfnqWwV7J6">via GIPHY</a></p>

On some level, I knew this lab would be an opportunity to challenge myself and remind me of how far I'd come. Prior to starting the lab, I had to download and configure alot. I downloaded .atom, ruby, Git Bash and Github. After syncing my files with my github account, and creating a repository, it began! Watching [Avi Flobaum's video](https://www.youtube.com/watch?v=_lDExWIhYKI) really helped. He recommended some neat tricks like using bundler, or making sure certain gems are installed;

```

gem install pry #> enables debugging
gem install HTTParty #>scraps HTML and CSS from a webpage
gem install nokogiri #>stores scraped HTML/CSS as a Nokogiri object
gem install bundler #> initiates a 'starter pack' of files to create a gem or app

```


#### Programming involves a lot of planning. Here are some things to consider;

```
1. Plan your interface - how will it interact with users?

2. Start with the project structure 

3. Start with the entry point (the file run)

4. Leverage the entry point to begin building out the CLI interface

5. Start making things real - instantiate objects

6. Integrate your objects with your CLI interface

7. Test run your program as needed 

8. Debug and tweak as needed

9. Rinse and repeat!
```


#### I outlined my goals and expectations;

```
Notes to self; 

1. User types articles
  - 'articles' initiates a file that executes the program [executable]
  
2. Program shows a numbered list of articles
  - I.e;
      - 1. <article title 1>, URL <URL>
      - 2. <article title 2>, URL <URL>
      - 3. ...etc...
      
3. Program puts "Which article do you want to read?"
  - Note to self =
      - will program select the article based on the number in the list? or based on name?
      - need to indicate such in, "Which article do you want to read?"

~. An article has; [UI]
  - Title
  - link
```

I decided to scrape the blog [Technical.ly ](https://technical.ly/dc/). It reports on local tech industries in DC, Baltimore, Boston, Philadelphia and Delaware.


### So let's explore my steps for creating this app.

<iframe src="https://giphy.com/embed/3o7aCTXVcHJgJ4yoeI" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/funny-cartoon-kid-3o7aCTXVcHJgJ4yoeI">via GIPHY</a></p>


**Step1: What command invokes this app?**

`./bin/cli-app`

This doesn't mean `./bin/cli-app` has all of my code. It means that `./bin/cli-app` will call on at least one other file to run the files necessary. Since it's not a ruby file, I made sure it had `#!/usr/bin/env ruby`, so that when I called on a ruby file, or invoked a class, it would understand I was speaking the language of Ruby.

I decided to require a file in `lib`, since all of my files in `lib` are relevant to my app. Then I included `Initialize.new.call`. `Initialize` is a class, `.new` triggers the class to begin, and `.call` indicates that the class method `call` should be invoked first in the class of `Initialize`. My code looked like this;

```
#!/usr/bin/env ruby

require_relative '../lib/rube_cli_app'

Initialize.new.call
```

The file `../lib/rube_cli_app` invokes all code in the `lib` file. The file required `pry`, `nokogiri` and `open-uri` too;

```
require 'open-uri'
require 'nokogiri'
require 'pry'

require_relative "./cli_app_folder/version"
require_relative './cli_app_folder/cli'
require_relative './cli_app_folder/articles'
```


<iframe src="https://giphy.com/embed/SGrmNUjEHfVxC" width="480" height="324" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/monkey-pirate-walk-cycle-SGrmNUjEHfVxC">via GIPHY</a></p>


**Step2: How will your files interact with the user?**

This step was the easiest, and it helped me transition into the harder aspects of app creation. Inside of my `./lib/cli.rb` file, I created methods that returned strings to interact with users. Since I wanted my app to provide a list of articles, I made sure the strings communicated this;

```
class Initialize
  def welcome
    puts "-------------------------------------------------"
    puts "| ********************************************** |"
    puts "| ********************************************** |"
    puts "| ********************************************** |"
    puts "| *********WELCOME TO TECHNICAL.LY!!!!********** |"
    puts "| ********************************************** |"
    puts "| ********************************************** |"
    puts "| ********************************************** |"
    puts "-------------------------------------------------"

    puts "Are you ready to get your read ON?"
    puts "Carpe librum!"

    welcome_message
  end

def selection
      puts "Please enter the number of the article you would like to read,"
      puts "type ARTICLES to receive the complete list of articles,"
      puts "type BASKET to receive the list of articles you selected,"
      puts "or type EXIT to leave."
end

end
```

**But,** I needed to be able to initiate these strings to ensure a user received them. So I created a method that called on `#welcome` and `welcome_message`;

```
def call 
  welcome
  welcome_message
end
```

Do you see why `./bin/cli-app` invoked `Initialize.new.call`? Because it invokes methods that `puts` strings to support the user experience! Tah-dah!

<iframe src="https://giphy.com/embed/Fh3jgAvcn429W" width="480" height="383" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/Fh3jgAvcn429W">via GIPHY</a></p>


**Step 3: Scraping the webpage**

Scraping the webpage was the hardest part of coding. I almost exclusively used `binding.pry` to determine what `div` tag or `class` contained all of the general information I needed. I even played around with `element`, `value` or `text` to determine what code could pull specific bits of information from the webpage.

Then I used the `each` iterator to iterate through each code related to an individual article. This way it would scrape the article titles and URLs of each article. Fortunately whoever designed this webpage was systematic, so iterating through the articles was straightforward (once I figured out how to scrape titles and URLs).

I actually ended up scraping two parts of the same webpage. One section of the webpage was considered front-page news. The other section of the same webpage had breaking-news. I wanted to make sure all types of articles were included in the app, so the user would have a wider range to select from.

```

require 'nokogiri'
require 'HTTParty'
require 'pry'

class Articles

  def self.articles
    website = HTTParty.get("https://technical.ly/dc/")
    technically = Nokogiri::HTML(website)
    technically.css(".network-post-link")

    technically.css(".network-posts").children.each do |article|
        unless article.blank?
          url = article.attribute("href").value
          name = article.attribute("title").value.gsub("Read more about ", "")
          @@articles << self.new(name, url)
        end #unless loop
    end #each iteration


    technically.css(".latest-post-link").each do |article| 
      unless article.blank?
        url = article.attribute("href").value
        name = article.attribute("title").value.gsub("Read more about ", "").gsub("\u2019", "'")
        @@articles << self.new(name, url)
      end #unless loop
    end #each iteration

    @@articles = @@articles.uniq

  end #today method
	
	end
```


**Step 4:  Oscillating between cli.rb and articles.rb**

At this point, I transitioned back to `cli.rb`. Now that my class instance `@@articles` returned an array of instances of Articles scraped from the webpage, I could incorporate this in the user experience. For example;

```
class Initialize

  def call
    @articles = Articles.articles
    welcome
  end

  def list_articles
    puts "Check out these articles:"
    @articles.each.with_index(1) do |article, i|
        puts "#{i}."
        puts "Title: #{article.name}"
        puts "URL: #{article.url}"
    end #each iteration
  end
	
	end
	
```

I created the instance variable `@articles` and set it equal to `Articles.articles`, since `Articles.articles` returns `@@articles` inside of the Articles class. Then I created `#list_articles` to iterate through `@articles`, `puts`ing an interpolated string containing the article name and the URL.


**Step 5:  More oscillating!**

By this point I oscillated between `cli.rb`, `articles.rb` and `Pry`. Tweaking my code, testing it in Pry, and test running the CLI is the best approach at this point. It allows you to catch and debug smaller problems before they snowball into massive hurdles. I used this approach in every step of my coding process, but it became more and more important as I intergrated instantiated articles with the CLI.

<iframe src="https://giphy.com/embed/26BRHK4RwGJZGKVhK" width="480" height="288" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/pug-pirate-pooch-26BRHK4RwGJZGKVhK">via GIPHY</a></p>


**Major takeaways;**

* *The bigger the project, the more important the breaks.* As a web developer, projects won't get wrapped up in an hour or a day. Some projects take months or years to complete. Be okay with this.

* *Double-check everything through debugging and test runs.* It's easier to identify the root cause of an issue through incremental changes and test runs.

*  *Google it.* Sites like Stack Overflow, W3 and Ruby-Doc have consistently pointed me in the right direction. The resources are out there for a reason.

Feel free to check out my code [here](https://github.com/eyosef/eden-cli-app/tree/master/cli_app), and get in touch with any questions or comments.


