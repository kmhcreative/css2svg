<h3>WHAT IS IT?</h3>
<p>A Javascript-based utility for converting CSS3 Gradients to SVG images to help maintain the same look in a website viewed in browsers that do not support CSS3 gradients but do support SVG graphics.</p>
<p>The CSS3 to SVG converter is pure JS and does not require any libraries (though you could certainly fork a version that does if you want).  It is also presented in a single HTML page to make it easy for 
anyone who wants to use it or work on it offline to download it and know they have all the necessary code.</p>
<h1><a href="http://fiddle.jshell.net/CG9t2/1/show/light/">Try It!</a></h1>
<h3>HOW TO USE IT</h3>
<ol>
<li>Copy and paste almost any CSS3 Linear Gradient code into the input box at the top of the utility page.  It will accept W3C standards or Mozilla, Webkit (both old and new syntax), Opera, and Microsoft proprietary &#8220;vendor&#8221; versions <em>(see the &#8220;Release Notes&#8221; at the end of this page for details).</em></li>
<li>If you are converting a lot of gradients to SVGs then you&#8217;ll probably want to leave it so it automatically clears the input box each time you click in it to paste in a new string.  However, if you want to &#8220;play around&#8221; with the variables in the CSS code and see what changes you can turn off the auto-clearing feature.</li>
<li>Set a size for your SVG image.  Typically for tiled background images it is best to leave this at &#8220;percent&#8221; because it will automatically stretch and compress to fill the background of the element.  On the other hand if you know the gradient will fill the background of an element with a specific size you can set it in pixels instead.</li>
<li>Click the &#8220;Convert&#8221; button.</li>
<li>The source code for your SVG file appears in the output box.  Copy and paste it into any plain text editor and save it with the file extension &#8220;.svg&#8221; and you&#8217;ll have your SVG image file.</li>
<li>The &#8220;Preview&#8221; takes the same information in the source code and builds an actual SVG file into the page for you to see exactly how it will look.  Obviously your browser needs to support SVG images for this to work!<br />
<em>Note to Firefox users: Your browser allows you to edit the source code and press the &#8220;Update&#8221; button and see a live update in the preview of your changes. </em></li>
</ol>
<h3>HOW IT WORKS</h3>
<p>First it parses the CSS gradient string into the component parts.  If the string uses words (such as top, top left, bottom, bottom left, left, right) to indicate rotation rather than degrees (i.e., 45deg) then it first normalizes the verbose parameters to their degree value equivalents.</p>
<p>Next it takes the angle in degrees and converts it to radians.  CSS3 gradients rotate in degrees, but Javascript rotates in radians, so it needs to convert the value first.</p>
<p>Once it has radians it then converts the result into vector coordinates.  SVG can rotate either in degrees or with vector coordinates.  You may be wondering why I didn&#8217;t just preserver the CSS degrees and use it for the SVG?  Well, it doesn&#8217;t give you exactly the same results as the vector coordinates.  With vector coordinates you can make sure the gradient properly fills the space.  SVG gradient rotation (with the <em>gradientTransform=rotate(n) </em>attribute) doesn&#8217;t change the length of the vectors. However, another problem I discovered was that certain angles didn&#8217;t map properly using the SVG rotate attribute!  It was most noticeable with 315 degrees and its mirror 135 degrees, but the problem affected all degrees within each of those quadrants of the circle.  The rotate attribute offers no real options to correct this so I had to get the vector coordinate method to work.</p>
<p>Initially I thought the script was wrong because I reasoned a 45 degree angle should have vector coordinates like this: <em>x1=&#8221;0%&#8221; y1=&#8221;100%&#8221; x2=&#8221;100%&#8221; y2=&#8221;0%&#8221; </em>but my script was producing this: <em>x1=&#8221;0%&#8221; y1=&#8221;70%&#8221; x2=&#8221;70%&#8221; y2=&#8221;0%&#8221;</em></p>
<p>Oddly enough at a small scale this still looks like a proper 45 degree angle.  So does its mirror of 225 degrees.  But when I made the CSS gradient fill the browser it became apparent that even in CSS3 gradients a 45 degree angle doesn&#8217;t <em>actually</em> hit at the corners of a square &#8211; it&#8217;s slightly offset just like the SVG images.</p>
<p>But the vector coordinates suffered the same problem as the rotation attribute in that 135 degrees, 315 degrees, and all the other degrees within their quadrants were offset from where they should be.</p>
<p>CSS3 Gradient: <em>background: -webkit-linear-gradient(135deg, #779ae8 0%,#376fe0 50%,#2260dd 51%,#3690f0 51%,#2463de 100%);</em></p>
<p>SVG Rotation: <em>&lt;linearGradient id=&#8221;grad&#8221;  gradientTransform=&#8221;rotate(135)&#8221; &gt; </em>or SVG Vector:<em> &lt;linearGradient id=&#8221;grad&#8221;  x1=&#8221;70%&#8221; y1=&#8221;70%&#8221; x2=&#8221;0%&#8221; y2=&#8221;0%&#8221;&gt;</em></p>
<p>After about a day of trying to figure out why this was happening I finally just settled on a hack to correct it.  The offset in both quadrants was consistent so in my checks for negative numbers I simply told it if it was a positive value for a degree setting that fell in between 90 and 180 degrees or between 270 and 360 to add .3 to the radians value before converting to vector coordinate percentages, which effectively turns each &#8220;70%&#8221; in the examples above to &#8220;100%.&#8221;  As you can see from the images above it fixes the problem perfectly, though I&#8217;m still not clear why it happens in the first place at least my converter now makes SVG image consistent with the CSS3 input.</p>
<p>The next thing the converter does it wraps all the parameters in the XML code needed to create the SVG source code.  Lastly it creates a SVG element in the page with the same parameters for the Preview.  <del>For Firefox users there&#8217;s an additional function because that browser supports creating the SVG preview image from the code in the output box &#8211; meaning you can edit that code in the output box, click &#8220;Update&#8221; and see your changes immediately reflected in the preview.  <em>Unfortunately this isn&#8217;t supported by any of the other browsers.</em></del> (See below, v0.9 supports more browsers).</p>
<h3>JSFiddle</h3>
<p>If you want to contribute to this project it is recommended you <a href="http://jsfiddle.net/CG9t2/1/">play around with the code in the JSFiddle</a> or offline and when you know your changes work 
then commit them here to GitHub.  The converter is intentionally presented as a single HTML page with all the CSS and scripting in it so anyone who wants to download it for editing or offline use can 
be assured they have ALL the necessary code.  From JSFiddle you should open the "full screen result" of your fiddling (URL available under the "Share" button), and when you look at the source code make 
sure you are viewing it for the IFRAME in which the result is shown (you may need to right+click > show only this frame).  JSFiddle also adds a dummy script and css link to the top of the document which 
do not need to be included in the git commit and please change the title of the document:</p>
<blockquote>
 <p>&lt;title&gt; - jsFiddle demo&lt;/title&gt;<br/>  
    &lt;script type='text/javascript' src='/js/lib/dummy.js'&gt;&lt;/script&gt;<br/>  
    &lt;link rel="stylesheet" type="text/css" href="/css/result-light.css"&gt;</p>
</blockquote>
<h3>RELEASE NOTES</h3>
<p><em>Version 0.9.5</em> (May 27, 2013)</p>
<p>Overview of major changes, done by Anthony Martinez (http://www.linkedin.com/in/canthonymartinez/). (All other script/CSS Annotations by me are preceded by "AM:")</p>
<ol>
<li>Added an optional batch mode to generate base64 CSS output for multiple selectors at once. Yes! Another exclusive feature, as far as I know. Born out of frustration with the limitations of existing LESS mixins and online gradient generators, this blows everything out of the water :) Requires IE10 or any recent release of Chrome, FF, Safari, or Opera; it won't work in IE9-.</li>
<li>Optimized IE9 base64 output to retain original rgba/hsla/transparent colors, saving a few extra bytes per stop.</li>
<li>Migrated all JS event handlers into the < script > block to separate content and behavior.</li>
</ol>
<p><em>Version 0.9</em> (May 26, 2013)</p>
<p>Overview of major changes, done by Anthony Martinez (http://www.linkedin.com/in/canthonymartinez/). All other script/CSS Annotations by him are preceded by &#8220;AM:&#8221;</p>
<ol>
<li>Added full support for new unprefixed W3C syntax gradients (using &#8216;to &lt;destination&gt;&#8217; syntax).</li>
<li>Added logic to calculate degrees differently, to match the new W3C syntax.For example, try -moz-linear-gradient(72deg,#fff,#000) and linear-gradient(72deg,#fff,#000) in CSS &#8212; they render differently.Then input them into this script, and they should each render in SVG the same way they do in CSS.</li>
<li>If all color stop percentages are missing, then the script will now interpolate them, as happens in CSS.If only the start and ending stops are missing, the script will add them.</li>
<li>If no directions or angle units are specified, the script will now assume defaults, as happens in CSS.</li>
<li>&#8220;Angle units&#8221;? Yeah, there&#8217;s now support for all valid units, (deg, rad, grad, &amp; turns). Plus negative values and decimals work.</li>
<li>Improved support for old Webkit syntax &#8212; from() and to() will work as expected, even with decimals, and even if to() comes before other color-stops (as is acceptable).</li>
<li>Added support for RGB/A percents, HSL/A, floating points in RGB/A and HSL/A, color names, and &#8216;transparent&#8217; keyword.</li>
<li>Added logic to convert alpha values and &#8216;transparent&#8217; to proper SVG &#8216;stop-opacity&#8217; values.</li>
<li>Overhauled the SVG vector generation logic, greatly improving accuracy.</li>
<li>Added optional IE9 base64 output for CSS.</li>
<li>Added multiple background support. Yes! No other SVG or gradient generator I&#8217;m aware of, even the awesome visualcsstools.com that I drew inspiration from, has this.</li>
<li>Extended SVG preview display/update capabilites to all capable browsers (Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+)</li>
</ol>
<p>Known Issues:</p>
<ol>
<li>Still no radial-gradient support yet, but I plan to figure that out not too long from now!</li>
<li>For some reason, FF3.6 and below can only do one conversion per page load/refresh. Those browsers are ancient, though. So, perhaps they&#8217;re not worth trying to fix? It&#8217;s odd, though. Even IE7 works the script flawlessly!</li>
<li>Older browsers that don&#8217;t fully support RGBA or HSL/A will trip on the color validation loop I included, if input gradient(s) has/have RGBA and/or HSL/A.</li>
</ol>
<p>&nbsp;</p>
<p><em>Version 0.1 (<a href="http://www.kmhcreative.com/downloads/CSS2SVG/">Archived</a>)</em></p>
<p>Preview does not work in Internet Explorer, however the source code output does so you can still make SVG images with it.</p>
<p>CSS3 Gradient parameters that are <span style="color: #800000;"><strong>NOT</strong></span> supported:</p>
<ul>
<li>color stops expressed as decimals (ex. &#8220;0.7&#8243;) instead of percentages (ex. &#8220;70%&#8221;)</li>
<li>The old webkit &#8220;from&#8221; and &#8220;to&#8221; syntax is not supported.  So this will not work:<br />
<em>-webkit-gradient(linear, 0% 0%, 0% 100%, from(#666666), to(#666666), color-stop(.6,#333))<br />
</em>However, the old syntax in this format IS supported:<br />
<em>background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#666666), color-stop(100%,#666666), color-stop(60%,#333333));</em></li>
<li>No support for &#8220;hsl&#8221; or &#8220;hsla&#8221; color stops.  Only &#8220;hex,&#8221; &#8220;rgb&#8221; and &#8220;rgba&#8221; are supported.  However &#8220;rgba&#8221; (alpha channel) support varies across browsers so you will probably want to change them to &#8220;rgb&#8221; instead for better compatibility.</li>
<li>The converter currently does not support &#8220;radial&#8221; gradients at all!</li>
</ul>
<h3>ACKNOWLEDGEMENTS</h3>
<p>I&#8217;m not very good with math so I would never have been able to figure out how to build this without the following:</p>
<p><a href="http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle">http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle</a></p>
<p><a href="http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and">http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and</a></p>
<p><a href="http://www.codeproject.com/KB/books/learnsvgchapter07.aspx">http://www.codeproject.com/KB/books/learnsvgchapter07.aspx</a></p>
<p>HUGE thanks to Anthony Martinez for his additions to this!  <a href="http://www.linkedin.com/in/canthonymartinez/" target="_blank">http://www.linkedin.com/in/canthonymartinez/</a></p>
<h3><strong>LICENSE</strong></h3>
<p>Free to use, modify, improve, distribute, or do whatever you want with it.  I&#8217;d appreciate a link back here or attribution though.</p>
