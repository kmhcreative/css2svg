<h3>WHAT IS IT?</h3>
<p>A JavaScript-based utility for converting CSS3 Gradients to SVG images to help maintain a website's appearance in browsers that do not support CSS3 gradients but do support SVG graphics (such as Internet Explorer 9).</p>
<p>The CSS3 to SVG converter is pure JS and does not require any libraries (though you could certainly fork a version that does if you want).  It is also presented in a single HTML page for easy usage and editing.</p>
<h1><a href="http://jsfiddle.net/AnthonyM1229/CG9t2/3/show/light/" target="_blank">Try It!</a></h1>
<h3>BASIC USAGE INSTRUCTIONS</h3>
<ol>
<li>Copy and paste any CSS3 Linear Gradient code into the input box at the top of the utility page.  It will accept W3C unprefixed syntax and Mozilla, Webkit (both old and new syntax), Opera, and Microsoft proprietary vendor prefixes <em>(see the "Release Notes"; at the end of this page for details). It will even accept multiple gradients at once (new in 0.9.0).</em></li>
<li>If you are converting a lot of gradients to SVGs, then you'll probably want to mark the "Clear Input on Focus" checkbox so it automatically clears your input each time you click in it to paste a new string.  Otherwise, if you want to fiddle with the variables in the CSS and see what will change in the output, you should leave the auto-clearing feature off.</li>
<li>Set a size for your SVG image.  Typically for tiled background images, a percentage size is best because it will automatically stretch to fill the background of the element.  On the other hand, if you know the gradient is to fill the background of an element with a specific size, you can leave it as pixel-based dimensions. For accurate rendering of angles, pixel dimensions are recommended.</li>
<li>Click the "Convert" button.</li>
<li>The source code for your SVG file appears in the output box. Copy and paste it into any plain text editor and save it with the ".svg" file extension, and then you''ll have your SVG image file.</li>
<li>The "Preview" output box takes the same information in the source code and builds an actual SVG file into the page for you to see exactly how it will look.  You may also edit the source code and press "Update" to see the preview with your changes. <em>Please note the browser compatibility list: older browsers may not support the SVG preview/editing functionality.</em></li>
</ol>
<h3>ADVANCED USAGE TECHNIQUES</h3>
<ol>
<li><b>CSS Output for IE9</b> (Added in 0.9.0)<br> Mark the "Generate CSS for IE9 (Base64 Output)" checkbox before clicking "Convert", and then along with the standard SVG output, you'll see another text box with base64 output. This takes the text of the SVG file and embeds it, so you can then plug it into your CSS file without the need of adding another HTTP request for an image file. <em>Note that this feature is IE9-specific. If you want to apply an SVG file as base64 to all browsers, then feel free to paste the SVG output text at <a href="http://decodebase64.com/">decodebase64.com</a> to get cross-browser base64 output.</em></li>
<li><b>Batch Mode</b> (Added in 0.9.5)<br> Mark both the "Generate CSS for IE9 (Base64 Output)" and "Batch Mode" checkboxes, and you'll enable a special mode that lets you convert a whole bunch of gradients at once! Mark these checkboxes before adding any text input, and you'll see an example of how to use Batch Mode, show up in the input text box. Just paste your CSS selectors (containing only gradients) in the input, click "Convert", and you'll see base64 output for each selector appear in the output below. There is no preview or code updating enabled while Batch Mode is active, however.
</li>
</ol>
<h3>HOW THE SCRIPT WORKS</h3>
<p>Check out the embedded comments in the script for further explanations of the steps it carries out. In short, the script</p>
<ol>
<li>parses input gradient(s) to separate angles or origin/destination keywords and individual color stops;</li>
<li>calculates SVG vector coordinates based on the angles or keywords;</li>
<li>generates color stops with your specified colors and offsets (or calculates missing offsets);</li>
<li>and finally builds an SVG file with the complete gradient(s).</li>
</ol>
<h3>JSFiddle</h3>
<p>If you want to contribute to this project, then we recommend you <a href="http://jsfiddle.net/AnthonyM1229/CG9t2/3/" target="_blank">play around with the code in the JSFiddle</a> or offline and when you know your changes work 
then commit them here to GitHub.  The converter is intentionally presented as a single HTML page with all the CSS and scripting in it so anyone who wants to download it for editing or offline use can 
be assured they have ALL the necessary code.  From JSFiddle, you should open the "full screen result" of your fiddling (URL available under the "Share" button), and when you look at the source code make 
sure you are viewing it for the IFRAME in which the result is shown (you may need to right+click > show only this frame).  JSFiddle also adds a dummy script and css link to the top of the document which 
do not need to be included in the git commit and please change the title of the document:</p>
<blockquote>
 <p>&lt;title&gt; - jsFiddle demo&lt;/title&gt;<br/>  
    &lt;script type='text/javascript' src='/js/lib/dummy.js'&gt;&lt;/script&gt;<br/>  
    &lt;link rel="stylesheet" type="text/css" href="/css/result-light.css"&gt;</p>
</blockquote>
<h3>RELEASE NOTES</h3>
<em>Current Browser Support:</em>
<ul>
<li><b>Full Support: </b> Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+</li>
<li><b>SVG Preview/Editing Unavailable</b>: Chrome 6-, IE8-, FF3.6-, Safari 5.0-, Opera 11.5-</li>
<li><b>Limited Support (can only do one conversion per page load/refresh):</b> FF3.6-, Opera 10-</li>
</ul>
<p>Overview of major changes, done by Anthony Martinez. (All script/CSS annotations by him in the script file download are preceded by "AM:")</p>
<p><em>Version 0.9.6</em> (May 28, 2013)</p>
<ol>
<li>Improved support for IE9-. They can now generate CSS base64 output and execute Batch Mode, thanks to the tiny shim he found for the <code>window.btoa</code> function.</li>
<li>Improved error-handling in Batch Mode. If any individual gradients return an error, processing continues to the end, and those gradients that returned an error are noted in the output.</li>
<li>Improved support for IE8-, FireFox 2-, Safari 3.0-, and Opera 9.6-. They will now skip over the CSS color validation loop, thereby avoiding any errors caused by having RGBA and/or HSL/A colors in the input gradient(s). Fixes issue #3 on the bottom.</li>
<li>Bug fix for IE8-: most input color names smaller than 8 letters would output a dud string in the SVG. Now the input color names get output as is, as expected.</li>
</ol>
<p><em>Version 0.9.5</em> (May 27, 2013)</p>
<ol>
<li>Added an optional batch mode to generate base64 CSS output for multiple selectors at once. Yes! An exclusive feature, as far as he knows. Born out of frustration with the limitations of existing LESS mixins and online gradient generators, this blows everything out of the water :) Requires <del>IE10</del> <ins>IE9</ins> or any recent release of Chrome, FF, Safari, or Opera; <del>it won't work in IE9-</del>.</li>
<li>Optimized IE9 base64 output to retain original rgba/hsla/transparent colors, saving a few extra bytes per stop.</li>
<li>Migrated all JS event handlers into the <code>&lt;script&gt;</code> block to separate content and behavior.</li>
</ol>
<p><em>Version 0.9.0</em> (May 26, 2013)</p>
<ol>
<li>Added full support for new unprefixed W3C syntax gradients (using <code>to &lt;destination&gt;</code> syntax).</li>
<li>Added logic to calculate degrees differently, to match the new W3C syntax.For example, try <code>-moz-linear-gradient(72deg,#fff,#000)</code> and <code>linear-gradient(72deg,#fff,#000)</code> in FireFox CSS &#8212; they render differently.Then input them into this script, and they should each render in SVG the same way they do in CSS.</li>
<li>If all color stop percentages are missing, then the script will now interpolate them, as happens in CSS. If only the start and ending stops are missing, the script will add them.</li>
<li>If no directions or angle units are specified, the script will now assume defaults, as happens in CSS.</li>
<li>"Angle units"? Yeah, there's now support for all valid units, (<code>deg</code>, <code>rad</code>, <code>grad</code>, &amp; <code>turn</code>). Plus negative values and decimals work.</li>
<li>Improved support for old Webkit syntax &#8212; <code>from()</code> and <code>to()</code> will work as expected, even with decimals, and even if <code>to()</code> comes before other color-stops (as is acceptable).</li>
<li>Added support for RGB/A percents, HSL/A, floating points in RGB/A and HSL/A, color names, and <code>transparent</code> keyword.</li>
<li>Added logic to convert alpha values and <code>transparent</code> to proper SVG <code>stop-opacity</code> values.</li>
<li>Overhauled the SVG vector generation logic, greatly improving accuracy.</li>
<li>Added optional IE9 base64 output for CSS.</li>
<li>Added multiple background support. Yes! No other SVG or gradient generator he's aware of, even the awesome visualcsstools.com that he drew inspiration from, has this.</li>
<li>Extended SVG preview display/update capabilites to all capable browsers (Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+)</li>
</ol>
<h3>KNOWN ISSUES:</h3>
<ol>
<li>Still no radial-gradient support yet, but he plans to figure that out eventually!</li>
<li>For some reason, FF3.6 and below (and Opera 10 and below) can only do one conversion per page load/refresh. Those browsers are ancient, though. So, any fixes for them will be of lowest priority for us, but you're welcome to contribute a fix! This issue is odd, though. Even IE7 can do multiple conversions! Heck, so can IE6!</li>
<li><ins>&#8212;Fixed in 0.9.6&#8212;</ins> <del>Older browsers that don&#8217;t fully support RGBA or HSL/A will trip on the included color validation loop, if input gradient(s) has/have RGBA and/or HSL/A.</del></li>
</ol>
<h3>ROADMAP</h3>
<p>Anthony intends to continue updating this script as time allows. Here's what he plans to implement:</p>
<p><em>Version 1.X</em>
<ol>
<li><code>canvas</code> output support, to facilitate converting SVG output into bitmap images (e.g., PNG) that IE8- and other ancient browsers lacking SVG support can read.</li>
</ol>
<p><em>Version 2.X</em></p>
<ol>
<li>Radial gradient support.</li>
</ol>
<h3>ARCHIVED VERSIONS</h3>
<p><em><a href="http://www.kmhcreative.com/downloads/CSS2SVG/">Version 0.1</a></em></p>
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
<p>Original Project Page: <a href="http://www.kmhcreative.com/labs/css3-2-svg/" target="_blank">http://www.kmhcreative.com/labs/css3-2-svg/</a></p>
<p>I&#8217;m not very good with math so I would never have been able to figure out how to build this without the following:</p>
<p><a href="http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle">http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle</a></p>
<p><a href="http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and">http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and</a></p>
<p><a href="http://www.codeproject.com/KB/books/learnsvgchapter07.aspx">http://www.codeproject.com/KB/books/learnsvgchapter07.aspx</a></p>
<p>HUGE thanks to Anthony Martinez for his additions to this!  <a href="http://www.linkedin.com/in/canthonymartinez/" target="_blank">http://www.linkedin.com/in/canthonymartinez/</a></p>
<h3><strong>LICENSE</strong></h3>
<p>Free to use, modify, improve, distribute, or do whatever you want with it.  I&#8217;d appreciate a link back here or attribution though.</p>
