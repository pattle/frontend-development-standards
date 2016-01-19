This is the CSS section of the front-end development standards

### Use a CSS reset

Every browser has a built in base stylesheet that applies default styles to elements when the page is loaded.  It's why if you don't provide your own stylesheet you can still differentiate between a `<h1>` and a `<p>`, however this base stylesheet varies from browser to browser.  There are arguments for and against using a reset but it's a good way of reducing the chance of browser inconsitencies.  The following is a list of widely used CSS reset's.  

- [normalize.css](https://necolas.github.io/normalize.css/)
- [Eric Meyer's CSS reset](http://meyerweb.com/eric/tools/css/reset/)
- [HTML5 Doctor Reset](http://html5doctor.com/html-5-reset-stylesheet/)

###Keep your CSS organised

Stylesheets can get very big very quickly which can make them troublesome to maintain.  If you want to alter the CSS for your site's footer it's a lot harder to locate the code you need to change if all your CSS is in the same file.  Therefore it's a good idea to seperate out your CSS into smaller files.  I commonly use the following file structure

````css
/* CSS Reset */
@import url("reset.css");

/* My default for base elements */
@import url("defaults.css");

/* Helper classes for common styles */
@import url("helpers.css");

/* Styles for common layout elements (e.g Header, Navigation, Footer) */
@import url("layout.css");

/* Style for section of the site I'm working on, these are examples */
@import url("home.css");
@import url("blog.css");

/* Responsive styles */
@import url("responsive.css");
````

After creating these four stylesheets I then like to componentise any remaining CSS.  If I'm working on a news section of a site I'll create a news.css stylesheet.  

Organising your CSS at the start of a project is a lot easier that trying to do it halfway through, so find a logical file structure that works for you and stick to it.  

### Keep a top down structure

Try to keep your CSS selectors in the order that they appear in your HTML so for example make sure that any header styles appear before footer styles.  

````css
header {
	/* Header style */
}

footer {
	/* Header style */
}
````

This just keeps your HTML and CSS in sync.  

### Minify your CSS
There are tools like [Grunt](http://gruntjs.com/) and [Gulp](http://gulpjs.com/) that will do this for you automatically whenever you modify and save a file.  

### Don't mix relative and non relative units

When setting font-size and line-height don't mix relative and non relative units.  The following is bad

````css
h4 {
	font-size: 1.2rem;
	line-height: 15px;
}

p {
	font-size: 15px;
	line-height: 1.5rem;
}
````

Instead you should do

````css
h4 {
	font-size: 1.2rem;
	line-height: 1.3rem;
}
````

#### Using rem's and pixels

Root ems have slightly better browser support than ems but to maximise support you can define the font size in pixels as a fallback.  If you set the base font size on the html element as 62.5% you can then define the font size in pixels followed by the same value divided by 10 in rems.  

````css
html {
	font-size: 62.5%;
}

body {
	font-size: 15px; /* Fallback for older browsers */
	font-size: 1.5rem;
}

h1 {
	font-size: 24px; /* Fallback for older browsers */
	font-size: 2.4rem;
}
````

Thanks to [discodavey](https://github.com/discodavey) for this one.  

### Style by class not id

To minimise the size of your CSS files try to avoid styling element by id and use classes instead.  The beauty of classes is that you can resuse them as much as your want so move styles into classes to avoid duplication

	<div id="my-element">Some content</div>

	#my-element {
		float: left;
		padding: 10px 5px;
		background: red;
		border-radius: 5px 5px 0 0;
		-moz-border-radius: 5px 5px 0 0;
		-webkit-border-radius: 5px 5px 0 0;
	}

Let's move some of those styles that we are likely to use again and create classes which we can apply to our `<div id="my-element"></div>`

	<div id="my-element" class="float-left curved-top"></div>	

	.float-left {
		float: left;
	}

	.curved-top {
		border-radius: 5px 5px 0 0;
		-moz-border-radius: 5px 5px 0 0;
		-webkit-border-radius: 5px 5px 0 0;
	}

	#my-element {
		padding: 10px 5px;
		background: red;
	}

In the future you can then reuse those classes on other element thus cutting down on the amount of CSS needed.  

If you are using LESS or SASS you can use mixins to add in properties from existing styles.  

### Don't specify units for 0 values

The CSS specification states that you shouldn't specify units when using 0 values and as they have no purpose its best to omit them.  

````css
/* Bad */
p {
	margin: 0px 0px 15px 0px;
}

/* Good */
p {
	margin: 0 0 15px 0; /* It's also easier to read */
}
````

### Don't name your selectors after colours

This goes for anything that may change over time.  Consider the below example

````css
.orange-link {
	color: orange;
}
````

Colours are typically something that are changed regulary and tweaked by clients.  If they decide the primary colour they want for links is red instead of orange then our class is now misleading.  You could change the class name but then you'd have to replace every instance of this class in your HTML or the chances are it would remain  `.orange-link` and cause confusion to future developers.