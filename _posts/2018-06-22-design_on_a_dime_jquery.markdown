---
layout: post
title:      "Design on a Dime: jQuery"
date:       2018-06-22 21:57:25 +0000
permalink:  design_on_a_dime_jquery
---


Adding jQuery front-end to my RoR app was a bit cathartic. The app was done - now it was off to improve the UI experience. Because I had nested my resources two levels deep, integrating jQuery was challenging. However, ultimately, I was able to find work-arounds that successfully made use of jQuery and enhanced the UX.

A more challenging aspect of this project was a Note to self feature users are able to implement on the user accounts. In addition to seeing their user reviews, users can submit notes on private thoughts they've had on businesses or products they've reviewed. Because the feature is simple, I decided jQuery would be perfect. It would allow a user to submit a few lines, and immediately see the object on their profile page. 

The first thing I did was use a `form_for` tag to create a form so users can submit their notes.  

```
<%= form_for @note, :url => { :controller => "notes", :action => "create"}, :html => {:method => :post} do |f| %>
    <%= f.label "Note to self:" %>
    <%= f.text_field :content %>
  
    <%= f.submit %>
  <% end %>
```

Once I did this, I updated my `notes#create` action so it could accept `json` and `html` requests. Since all new instances of notes would only be rendered through `json`, I only included `render json: @note, status: 201`. 

After this, I returned to my view and created `<script>` tags;

```
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js" ></script>
  <script type="text/javascript" charset="utf-8">
	</script>
```

The first script tag allows us to access all functions associated with jQuery. Without it, our code is useless. If you are using an HTML version 4 or less, `type="text/javascript"` helps specify that the JS language will be used here. Finally, `charset="utf-8"` integrates the Unicode standard, which is a coding system that supports global processing/display of text.

Now we can finally code in JS. Woohoo!

First thing's first: let's disable the form submit button;


```
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js" ></script>
  <script type="text/javascript" charset="utf-8">
  $(function () {
    $('form').submit(function(event) {
        event.preventDefault();
        });
    });
```

By calling on the form with `$('form').submit`, we're essentially  redirecting the submit button to this function, instead of to the controller.

` event.preventDefault();` is inside of this function. It stops the submit function from doing what it normally does; pass parameters to the controller. 

Once we do that, we need to remember our goal: to persist instantiated data to the user account page without refreshing. Even though we used `$('form').submit`, the object has been instantiated in the database. We're just using `render` in our action to prevent a page refresh.

Next, we need to pull the notes id of this object. How do we do that? `const values = $(this).serialize()`. We're setting a constant equal to a jQuery feature, `.serialize()`, which creates URL encoded text.

Then, we'll call on the instance of Note through `const posting = $.post("/notes", values)`. 

Finally. we can post it! Once the post is done `posting.done`, we can append the note to the document;

```
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js" ></script>
  <script type="text/javascript" charset="utf-8">
  $(function () {
    $('form').submit(function(event) {
        event.preventDefault();
				const values = $(this).serialize();
        const posting = $.post("/notes", values);
        
        posting.done(function(data) {
            const note = new Note(data.content);
            $("#notes").append(`<p> ${note.content} </p>`)
            $("#notes").append(`<div id=delete-${note.id}><button class="deleteButton" data-id=${note.id}>Delete</button></div>`)
        });
    });
```

Well, there you have it - it was hard, but worth it! I really enjoyed using jQuery. At first it was really hard and confusing, but it's grown on me and I can honestly say it's a pleasure to use.

To check out my repo, feel free to click [here](https://github.com/eyosef/spirited).
