### Don't hide core content on different devices

The device someone is using to view your website shouldn't affect what content they can and can't see.  When a section of content works great on desktop but not on mobile the solution isn't to hide it, because doing so will affect the user's experience.  You may need to put some more thought into *how* you're going to make it work across multiple devices and platform but this it extra work you should be willing to spend.  

### Target sizes

Apple reccommends the miniumum target size on mobile device should no less that 44 x 44 points, any smaller than this and elements can be harder to interact with.  This applies to links, inputs, buttons, etc.  

### Look for common breakpoints

There's a wide variety of devices on the market and with that comes a wide variety of screen sizes.  When deciding what breakpoints to use find out what devices are popular among users of your site and find common breakpoints that will work well for them all.  [mydevice.io](http://mydevice.io/devices/) has a list of common devices and their screen sizes.  The value you want to use is the CSS width.  

````css
@media (max-width: 375px) {
	/* Target iPhone 6 */
}
````