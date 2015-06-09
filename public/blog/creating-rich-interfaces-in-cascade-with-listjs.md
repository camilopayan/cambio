# Creating rich interfaces in Cascade with List.js

So a common problem I run into with Cascade is that we'd need a page with a lot of similar content
that needs to be searchable, sortable, the works. In the past, we've accomplished this by having a
few php files, a backend interface for adding and removing items, and a database to hold our information.

Why do that, when we can use a little of what Cascade does best: leveraging XSLT/Velocity to transform data, and
using a great Javascript library called [List.js](http://www.listjs.com/)?

The great thing about List.js is that it'll wire up searching and sorting client-side with any
list that contains the metadata that needs to be searched or sorted on. For example, on the
[FIU Social website](social.fiu.edu), the social media accounts are organized into an unordered list, where 
the list items look like this:

    <li>
	 	<img src="_assets/images/offices-services/bbccampuslife.png">
		<h3 class="name">
			<a href="http://bbcclo.fiu.edu/">Campus Life at Biscayne Bay Campus</a>
		</h3>
		<p>The Department of Campus Life provides a variety of programs and services to the students and University community</p>
		<p class="social-links">
			<a class="webicon facebook" href="https://www.facebook.com/CampusLifeBBC">facebook</a>
		</p>
		<p class="categories">Offices and Services</p>
	</li>

When it comes to List.js, after telling it where to look for the list for searching and sorting. The classes with data
are passed to List.js like so:

    
	 var options = {
		valueNames: [ 'name', 'facebook', 'twitter', 'tumblr', 'instagram', 'vine', 'categories' ],
		listClass: 'social-list'
	 };

	 var socialList = new List('socials', options);

List.js will even search through the parts of your HTML that are hidden, like, in this case, the `categories` class.
Moreover, a search bar inside the id given to List.js will be wired up to search the list. In this case, we passed a 
`socials` id was sent to List.js. Inside is the listClass `social-list` which holds our data. There is also a search 
input with class `search` that will serve as our search bar. 

The HTML looks like this: 

    <div id="socials">
	 	<input class="search" placeholder="Search" type="text">
		<ul class="social-list">
		[...]
		</ul>
	 </div>

And there you go. A nice interface that can still be used from Cascade. List.js is pretty fast and doesn't have any trouble
with a responsive, semantic setup.
