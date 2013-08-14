<h1>What Is It?</h1>
<p>CSS2SVG is a JavaScript-based utility for converting CSS3 Gradients to SVG images to help maintain a website's appearance in browsers that do not support CSS3 gradients but do support SVG graphics (such as Internet Explorer 9).</p>
<p>The script is pure JS and does not require any libraries (though you could certainly fork a version that does if you want). It is also presented in a single HTML page for easy usage and editing.</p>
<h2><a href="http://jsfiddle.net/camartinez1229/thSxh/show/light/" target="_blank">Try It!</a></h2>
<h2>Basic Usage Instructions</h2>
<ol>
<li>For offline usage, download CSS2SVG.htm from the file listing above; that's the only file you need!</li>
<li>Copy and paste any gradients into the input box at the top of the script page. <code>linear-gradient</code> and now <code>repeating-linear-gradient</code> <em>(new in Version 1.5.0)</em> are supported, with or without prefixes.</li>
<li>If you're converting many gradients, then you may want to mark the "Clear Input on Focus" checkbox to expedite pasting/typing new gradients.</li>
<li>Declare a size. Typically for tiled background images, a percentage is best because it will stretch to fill the element's background. However, if you know the gradient is to fill the background of an element with a specific size, you can leave it as pixel-based dimensions. <em>For accurate rendering of angles, pixels are recommended.</em></li>
<li>Click "Convert".</li>
<li>Copy and paste the SVG output into any plain text editor and save it as an <kbd>.svg</kbd> file.</li>
<li><b>That's all you have to do!</b> You'll also see that the "Preview" section takes the same code in your output and inserts an actual SVG file into the page for you to see how the image will look. If you're not satisfied with the appearance, or you just want to change it, then edit the output and click "Update" to refresh the preview. <em>Please note the browser compatibility list; older browsers may not support the SVG preview/editing functionality.</em></li>
</ol>
<h2>Gradient Test Cases</h2>
<p><a href="https://github.com/camartinez1229/css2svg/blob/master/gradient-test-cases.md">Check out some sample gradients</a> to work with to demonstrate the script's functionality.</p>
<h2>Advanced Usage Techniques</h2>
<p><a href="https://github.com/camartinez1229/css2svg/blob/master/advanced-usage-techniques.md">Check out advanced usage documentation here.</a></p>
<h2>How the Script Works</h2>
<p>Check out the embedded comments in the script for further explanations of the steps it carries out. In short, the script</p>
<ol>
<li>parses input gradient(s) to separate angles or origin/destination keywords and individual color stops;</li>
<li>calculates SVG vector coordinates based on the angles or keywords;</li>
<li>generates color stops with your specified colors and offsets (or calculates missing offsets);</li>
<li>and finally builds an SVG file with the complete gradient(s).</li>
</ol>
<h2>JSFiddle</h2>
<p>If you want to contribute to this project, then we recommend you <a href="http://jsfiddle.net/camartinez1229/thSxh/" target="_blank">play around with the code in the JSFiddle</a> or offline, and when you know your changes work, then commit them here to GitHub. The converter is intentionally presented as a single HTML page with all the CSS and scripting in it, so, if you want to download it for editing or offline use, you can be assured you have ALL the necessary code. From JSFiddle, you should open the "full screen result" of your fiddling (URL available under the "Share" button), and when you look at the source code, make sure you are viewing it for the IFRAME in which the result is shown (you may need to right+click > show only this frame). JSFiddle also adds a dummy script and CSS link to the top of the document which 
do not need to be included in the git commit and please change the title of the document:</p>
<blockquote>
 <p>&lt;title&gt; - jsFiddle demo&lt;/title&gt;<br/> 
  &lt;script type='text/javascript' src='/js/lib/dummy.js'&gt;&lt;/script&gt;<br/> 
  &lt;link rel="stylesheet" type="text/css" href="/css/result-light.css"&gt;</p>
</blockquote>
<h2>Release Notes</h2>
<h3>Current Browser Support</h3>
<ul>
<li><b>Full Support: </b> Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+</li>
<li><b>SVG Preview/Editing Unavailable</b>: Chrome 6-, IE8-, FF3.6-, Safari 5.0-, Opera 11.5-</li>
</ul>
<h3>Overview of major changes, done by Anthony Martinez:</h3>
<h4><i>Version 1.5.4</i> (August 14, 2013)</h4>
<ol>
<li>Bug fix: Following the 1.5.3 update, gradients with any explicitly defined color-stops other than <code>calc</code> expressions were rarely if at all converting properly.</li>
</ol>
<h4><i>Version 1.5.3</i> (July 17, 2013)</h4>
<ol>
<li>Added support for CSS <code><a href="http://www.w3.org/TR/css3-values/#calc">calc()</a></code> expressions, e.g. <code>calc(100% - 75px)</code>, as gradient stop values. Nested <code>calc()</code> expressions are not supported, however.</li>
<li>Bug fix / improvement in error-handling: The script's color validation check was not always throwing an error when it should do so.</li>
</ol>
<h4><i>Version 1.5.2</i> (July 2, 2013)</h4>
<ol>
<li>Bug fix: Use of ID selectors in Batch Mode would sometimes cause the script to improperly throw an error message.</li>
</ol>
<h4><i>Version 1.5.1</i> (June 23, 2013)</h4>
<ol>
<li>Bug fix: Logic for calculating <code>repeating-linear-gradient</code> color-stops was not being triggered properly.</li>
<li>Bug fix: Error message was being thrown unnecessarily for gradients with no angle or origin/destination keywords defined.</li>
</ol>
<h4><i>Version 1.5.0</i> (June 23, 2013)</h4>
<ol>
<li>Significantly improved gradient stops calculation. Now, any gradient with any number of missing stops should get converted properly.</li>
<li>Added support for absolute units in gradient color-stops: you may now use <code>px</code>, <code>cm</code>, <code>mm</code>, <code>in</code>, <code>pt</code>, and <code>pc</code>.</li>
<li>Added experimental support for <code>repeating-linear-gradient</code>. The script produces output with correct angles (arguably the most important part); however, eagle-eyed observers will notice discrepancies from CSS rendering&#8212;this is especially the case when the first color stop is not equal to zero. Future updates may correct such discrepancies if possible.</li>
<li>Bug fix: Due to the way the script previously handled missing color-stops, some gradients with at least three stops, where the initial color-stop(s) is/are defined and the last two left off, were not rendering properly.</li>
<li>Bug fix: A temporary <code>div</code> variable used in converting color names to hex was not being cleaned up properly after execution, leading to accumulation of unneeded divs in the page DOM with multiple conversions.</li>
<li>Bug fix: Gradients with no angle or origin/destination keywords defined, with a color name at the first color-stop would not convert properly when the first color-stop is explicitly labeled (e.g., <code>linear-gradient(transparent 0%, ...)</code> were not working).</li>
<li>Bug fix / improvement in error-handling: <code>hsl/a</code> colors with hues >360 degrees were not converting to the proper color.</li>
<li>Bug fix / improvement in error-handling: The script was silently allowing hex colors not in proper three- or six-digit notation, instead of throwing an error in the color validation check.</li>
<li>Added further enhancements to the page's usability. Now, you can perform a conversion or update by pressing <kbd>shift</kbd>+<kbd>enter</kbd> inside the input/output <code>textarea</code>s, or pressing <kbd>enter</kbd> when the radio buttons, checkboxes, or dimension inputs have focus.</li>
<li>Despite the significant updates as listed above, the page code is now about 5% smaller compared to Version 1.2.0, thanks to various micro-optimizations.</li>
</ol>
<p><a href="https://github.com/camartinez1229/css2svg/blob/master/changelog.md">See Full Changelog Here</a></p>
<h2>Known Issues</h2>
<ol>
<li>Still no radial-gradient support yet, but Anthony plans to figure that out eventually!</li>
<li><ins>&#8212;Fixed in 1.2.0&#8212;</ins> <del>For some reason, FF3.6 and below (and Opera 10 and below) can only do one conversion per page load/refresh. Those browsers are ancient, though. So, any fixes for them will be of lowest priority for us, but you're welcome to contribute a fix! This issue is odd, though. Even IE7 can do multiple conversions! Heck, so can IE6!</del></li>
<li><ins>&#8212;Fixed in 0.9.6&#8212;</ins> <del>Older browsers that don't fully support <code>rgba</code> or <code>hsl/a</code> will trip on the included color validation loop, if input gradient(s) has/have <code>rgba</code> and/or <code>hsl/a</code>.</del></li>
</ol>
<h2>Road Map</h2>
<p>Anthony intends to continue updating this script as time allows. Here's what he plans to implement (subject to change):</p>
<h3>Version 2.X</h3>
<ol>
<li>Radial gradient support.</li>
</ol>
<h3>Version 3.X</h3>
<ol>
<li><code>canvas</code> output support, to facilitate converting SVG output into bitmap images (e.g., PNG) that IE8- and other ancient browsers lacking SVG support can read.</li>
<li>(Maybe?) A tabbed interface to group the SVG code output, data URI output, canvas output, and SVG preview into one central location.</li>
</ol>
<h2>Acknowledgments</h2>
<p>Original Project Page: <a href="http://www.kmhcreative.com/labs/css3-2-svg/" target="_blank">http://www.kmhcreative.com/labs/css3-2-svg/</a></p>
<p>I&#8217;m not very good with math so I would never have been able to figure out how to build this without the following:</p>
<p><a href="http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle">http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle</a></p>
<p><a href="http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and">http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and</a></p>
<p><a href="http://www.codeproject.com/KB/books/learnsvgchapter07.aspx">http://www.codeproject.com/KB/books/learnsvgchapter07.aspx</a></p>
<p>HUGE thanks to Anthony Martinez for his additions to this! <a href="http://www.linkedin.com/in/canthonymartinez/" target="_blank">http://www.linkedin.com/in/canthonymartinez/</a></p>
<h2><strong>License</strong></h2>
<p>The script is licensed under a <a href="http://creativecommons.org/licenses/by-sa/3.0/" target="_blank">Creative Commons Attribution-ShareAlike 3.0</a> license.</p>
