### Store common values in variables

Any values that you are going to repeat should be stored in variables so they are easier to maintain

/* Like class names don't name variables after colours */
@primary-colour: #ed4f4e;
@secondary-colour #3c763d;
@secondary-colour-alt: #3c763d;
@tertiary-colour: #31708f;

@image-directory: ~"/path/to/images/directory";

@screen-xs: 400px;
@screen-sm: 800px;
@screen-md: 1000px;
@screen-lg: 1200px;

@phone: ~"(max-width: @{screen-xs})";
@tablet: ~"(min-width: @{screen-xs}) and (max-width: @{screen-sm})";
@tablet-down: ~"(max-width: @{screen-sm})";
@tablet-up: ~"(min-width: @{screen-xs})";
@laptop: ~"(min-width: @{screen-sm}) and (max-width: @{screen-md})";
@laptop-down: ~"(max-width: @{screen-md})";
@laptop-up: ~"(min-width: @{screen-sm})";
@desktop~"(min-width: @{screen-lg})";

### Don't nest unnecessarily

Don't nest just for the sake of nesting as it makes your LESS files too verbose.  

Bad

````css
nav {
	border-bottom: 1px solid #cccccc;

	ul {
		li {
			a {
				color: #000000;
				text-decoration: none;
			}
		}
	}
}
````

Good

````css
nav {
	border-bottom: 1px solid #cccccc;

	ul a {
		color: #000000;
		text-decoration: none;
	}
}
````