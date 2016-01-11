This is the JavaScript section of the frontend style guide.

### Use setTimeout to delay scroll and resize event handlers

It's a common to attach a handler to a scroll or resize event.  For example you might want to show some content when the user has scrolled to a certain point on the webpage.  Below is an example of attaching a handler directly to the window scroll event but doing so is bad practice.  

	$(window).scroll(function() {
		var $nav = $('nav');

		//Check to see if we are over 100 pixels from the top of the page
		if($(window).scrollTop() > 100) {
			//Add a class to the nav element so we can fix it to the top of the screen
			if(!$nav.hasClass('fixed')) {
				$nav.addClass('fixed');
			}
		} else {
			$nav.removeClass('fixed');
		}
	});

It's bad practice because this event fires for every scroll movement, so scrolling the entire length of a web page can fire over 100 times depending on the length, it may well be more than that.  You can visually see this by placing a `console.log()` inside your handler.  If the event fires 100 times it means the code insider your handler will fire 100 times which is inefficient, instead we want to delay it.  

````javascript
var $App = {};
$App.hasScrolled = false
 
$(window).scroll(function() {
    $App.hasScrolled = true;
});
 
setInterval($App.checkNavigation, 200);

$App.checkNavigation = function() {
	if($App.hasScrolled === true) {
        $App.hasScrolled = false;
			var $nav = $('nav');
			if($(window).scrollTop() > 100) {
				if(!$nav.hasClass('fixed')) {
					$nav.addClass('fixed');
				}
			} else {
				$nav.removeClass('fixed');
			}
		}
	}
}
````

The above code sets a variable to true if the user has scrolled and there is an interval running every 0.2 seconds that checks the value of this variable.  If it's true it runs our code to check wether or not to make the navigation sticky.  

### Don't pollute the global namespace

In JavaScript you should always avoid polluting the global namespace when it's unnessacery.  The main reason for doing this is because global variables increase the chance of conflicts with other JS code.  It's not highly unlikely that if you are using jQuery you are also using a few third party plugins to add functionality to your site.  If you define a global variable called `$header` and a plugin you're using does the same thing you're going to get a conflict.   Below is an example of code that pollutes the global namespace.  

````javascript
$(function() {
	var $base_url = 'http://www.example.com';
	var $position_from_top_of_page = $(window).scrollTop();
	var $number_of_links = $("#nav a").length();

	//Event handlers and other code...
});
````

Rather than doing the above you should protect your globals and one way of doing that is to create a global object which you can then add properties and methods too.  	This doesn't totally eliminate the chance of conflicts but it does greater reduce that chance

````javascript
$(function() {
	//Create an object that we can add properties to
	var $App = {};
	var $App.base_url = 'http://www.example.com';
	var $App.position_from_top_of_page = $(window).scrollTop();
	var $App.number_of_links = $("#nav a").length();
});
````

Just because we've now protected these globals it still doesn't make the above code okay, you should avoid using globals even if their namespace is protected.  Below are a few more reasons why it's a bad idea.  

#### Global variables are slower than local variables

Using global variables is slower than using local variables because the intepreter (the browser is most cases) will first check the local scope to find variables before moving outwards.  When the code below is run the interpreter will expect to find the `$i` and `$number_of_links` variables defined inside our function so it will look there first.  However because we have defined them outside of our function the intepreter will have to look further afield thus increasing the execution time.  

````javascript
var $App.number_of_links = $("#nav a").length();
var $i;
$('#my-link').click(function(e) {
	for ($i = 1; $i <= $App.number_of_links; $i++) {
		//Do something
	}

	e.preventDefault();
});
````

This code would be better written like

````javascript
$('#my-link').click(function(e) {
	var $number_of_links = $("#nav a").length();
	var $i;
	for ($i =1; $i <= $number_of_links; $i++) {
		//Do something
	}

	e.preventDefault();
});
````

#### Global variables consume more memory than local variables

Global variables have to be always kept in memory whereas local variables will only exist in memory during the lifetime of the function call they are located in.  

### Don't use return false; to stop links firing.  

Bad

````javascript
$('#my-link').click(function() {
	return false;
});
````

Good

````javascript
$('#my-link').click(function(e) {
	e.preventDefault();
});
````


### Don't be overzealous when traversing through the DOM

#### Use ID's instead of classes when selecting elements.  

Take the example HTML below

````html
<div class="row">
	<div class="col-sm-6">
		<div id="intro-message" class="intro">Hello my name is Chris.  Please to meet you</div>
	</div>
</div>
````

It's a lot more overhead to select elements using classes because jQuery traverses through the whole DOM trying to find all the instances of this class.  So rather than doing 

````javascript
$('.row .col-sm-6 .intro').fadeIn();
````

Do this

````javascript
$('#intro-message').fadeIn();
````

### Cache jQuery selectors

In the example below we are making jQuery traverse through the DOM twice when we only ever want to do it once.  Once we've selected the element we want to work with, we should cache it to a variable.  

````javascript
$('#load-more').click(function(e){
	$('#divOne').fadeIn();

	if($something === true) {
		$('#divOne').addClass('class-one');
	} else {
		$('#divOne').addClass('class-two');
	}

	e.preventDefault();
});
````

Using this method would make the code look something like

````javascript
$('#load-more').click(function(e){
	var $divOne = $('#divOne').fadeIn();

	if($something === true) {
		$divOne.addClass('class-one');
	} else {
		$divOne.addClass('class-two');
	}

	e.preventDefault();
});
````

### Chain methods when possible

Rather than doing 

````javascript
$divOne = $("divOne");
$divOne.removeClass('active');
$divOne.show();
````

You should chain these method calls

````javascript
$divOne = $("divOne");
$divOne.removeClass('active').show();
````