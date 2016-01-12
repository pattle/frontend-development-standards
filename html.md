### Make your HTML semantic

Markup your content in a semantic way to allow search engines and screen readers to better understand the nature of the content.  Rather than using elements like `<div>` and `<span>` which don't have any meaning make use of HTML5's semantic elements.  Below is an example of what a webpage might have looked like pre HTML5 where id's are being used to state what each element contains.

```html
<div id="header">
	<!-- Header content -->
</div>
<div id="nav">
	<!-- Primary navigation -->
</div>
<div id="main-content">
	<div class="article">
		<h1>Learn about tigers</h1>
		<span>Posted on: 01/01/2016 </span>
		<p>This is the content of the article about tigers</p>
		<p>History</p>
		<p>Some text detailing the history of tigers</p>
	</div>
</div>
<div id="sidebar">
	<h4>Also in this section</h4>
	<a href="https://www.google.co.uk/search?q=tiger" title="Search Google for tigers">Tigers</a>
	<a href="https://en.wikipedia.org/wiki/Bengal_tiger" title="Visit Wikipedia to find out more about the Bengal tiger">Bengal tiger</a>
	<a href="http://www.savetigersnow.org/" title="Find out how to save tigers from extinction">Save tigers now</a>
</div>
<div id="footer">
	<!-- Footer content -->
</div>
```
Below is the same page but the HTML has now been written in a semantic way.  Both users and search engines can now understand what each element contains.


```html
<header>
	<!-- Header content -->
</header>
<nav class="primary">
	<!-- Primary navigation -->
</nav>
<main>
	<div class="article">
		<h1>Learn about tigers</h1>
		<span>Posted on: <time>01/01/2016</time></span>
		<p>This is the content of the article about tigers</p>
		<h2>History</h2>
		<p>Some text detailing the history of tigers</p>
	</div>
</main>
<aside id="sidebar">
	<h4>Also in this section</h4>
	<nav class="secondary">
		<ul>
			<li>
				<a href="https://www.google.co.uk/search?q=tiger" title="Search Google for tigers">Tigers</a>
			</li>
			<li>
				<a href="https://en.wikipedia.org/wiki/Bengal_tiger" title="Visit Wikipedia to find out more about the Bengal tiger">Bengal tiger</a>
			</li>
			<li>
				<a href="http://www.savetigersnow.org/" title="Find out how to save tigers from extinction">Save tigers now</a>
			</li>
		</ul>
	</nav>
</aside>
<footer>
	<!-- Footer content -->
</footer>
```

### Use the correct doctype declaration

````html
<!DOCTYPE html>
````

### Always add titles to links

For accessibility anchor tags should always have a title attributes that provide more detail about where the link is taking you.  Don't just repeat the anchor text so rather than doing

````html
<a href="http://www.bbc.co.uk" title="Click here">Click here</a>
````

Do the following.

````html
<a href="http://www.bbc.co.uk" title="Go to the BBC website">Click here</a>
````

### Always use alt attributes on images

To enable screen readers and search engine to more easily understand what your images contain use the alt attribute.  

````html
<img src="tiger.jpg" alt="Begnal tiger hunting in long grass" />
````

### Avoid inline CSS and JavaScript

````html
<a style="color: #333333; text-decoration: underline" onclick="openMap()">Contact us</a>
````

Inline styles make your HTML messy and harder to maintain.  

### Validate your HTML

If you're experiencing bugs or cross browers problems then validating your HTML is a good debugging tool.  You're less likely to get bugs in valid well formed documents.

Validating your HTML does require extra effort but its a good indication of quality and that you care about your craft.  

The W3C site has a [HTML validator](https://validator.w3.org/)