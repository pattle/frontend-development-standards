This is the images section of the front-end development standards

### Don't use bigger images that you need

This one is a bit of a no brainer but it often gets forgotten.  When using images don't make them any bigger than they will ever be displayed.  In the example below the container the image sits in has a maximum width set of 300px.  Therefore your image should be no bigger than 300px because it will never be displayed at that size.  By making it bigger than needed you're just making your users download a larger file.  

````css
.image-container {
	max-width: 300px;
}

````html
<div class="image-container">
	<img src="/path/to/image.jpg" alt="Image description" />
</div>
````

### Use SVG, its scalable!

For simple images such as icons consider using SVG.  You'll find that the file size is small and it can increase in size without losing quality because as the name says its scalable

### Aim for the smallest image size

PNG's are great because they support transparency but they also come at a cost of larger file size.  Think about what image type is appropriate for what you're doing and then select the correct one accordingly.  Always try to get the smallest image size possible.  Images shouldn't be used to achieve gradient effects as 99% of the time this can be done using CSS.  

### Don't hide images using display: none

When developing a responsive site you may have multiple versions of the same image in different sizes.  Depending on the size of the screen you show the correct image and hide the others.  Below is an example of this.  

````css
.show-for-small, .show-for-large {
	display: none;
}

@media (max-width: 700px) {
	.show-for-small {
		display: block;
	}
}

@media (min-width: 701px) {
	.show-for-large {
		display: block;
	}
}
````

````html
<img src="/path/to/small-image.jpg" alt="Description of image" class="show-for-small" />
<img src="/path/to/large-image.jpg" alt="Description of image" class="show-for-large" />
````

Even though one of the images will be hidden depending on the device you are using they will both be downloaded by the user, considering you won't ever see one of them this is bad practice.  

Instead you should apply the images as a backgrounds as this way round the image will only be downloaded when it needs to be shown.  

````css
@media (max-width: 700px) {
	.show-for-small {
		background-image: url('/path/to/small-image.jpg');
	}
}

@media (min-width: 701px) {
	.show-for-large {
		background-image: url('/path/to/large-image.jpg');
	}
}
````

````html
<div class="show-for-small">
	<!-- Content goes here minus image -->
</div>
<div class="show-for-large">
	<!-- Content goes here minus image -->
</div>
````
Or there is a better option...

### The picture element

The picture element solves the problem of responsive images.  Rather than having to use CSS the change the image for different breakpoints the picture element takes care of all of that for you.  It's smart so the browser only downloads the image it needs to display rather than all of them.  

````html
<picture>
   <source srcset="/path/to/large-image.jpg">
   <source media="(max-width: 700px)" srcset="/path/to/small-image.jpg">
   <source media="(min-width: 1200px)" srcset="/path/to/really-large-image.jpg">
   <img src="/path/to/large-image.jpg" alt="Large image description">
</picture>
````

### Don't put text in images

It's not accessible, it's harder to update.  Don't do it.  