<h1>What Is It?</h1>
<p>CSS2SVG is a JavaScript-based utility for converting CSS3 Gradients to SVG images to help maintain a website's appearance in browsers that do not support CSS3 gradients but do support SVG graphics (such as Internet Explorer 9).</p>
<p>The script is pure JS and does not require any libraries (though you could certainly fork a version that does if you want). It is also presented in a single HTML page for easy usage and editing.</p>
<h2><a href="http://jsfiddle.net/camartinez1229/thSxh/show/light/" target="_blank">Try It!</a></h2>
<h2>Basic Usage Instructions</h2>
<ol>
<li>Copy and paste any CSS3 linear gradients into the input box at the top of the utility page. It will accept W3C unprefixed syntax and <code>-moz-</code>, <code>-webkit-</code> (both old and new syntaxes), <code>-o-</code>, and <code>-ms-</code> prefixed syntaxes. It will even accept multiple gradients at once <em>(new in 0.9.0)</em>.</li>
<li>If you are converting a lot of gradients to SVG, then you may want to mark the "Clear Input on Focus" checkbox so it automatically clears your input each time you click in it to paste/type a new string. Otherwise, if you want to fiddle with the variables in the CSS and see what will change in the output, you should leave the auto-clearing feature off.</li>
<li>Set a size for your SVG image. Typically for tiled background images, a percentage size is best because it will automatically stretch to fill the background of the element. On the other hand, if you know the gradient is to fill the background of an element with a specific size, you can leave it as pixel-based dimensions. For accurate rendering of angles, pixel dimensions are recommended.</li>
<li>Click the "Convert" button.</li>
<li>The source code for your SVG file appears in the output box. Copy and paste it into any plain text editor and save it with the <kbd>.svg</kbd> file extension, and then you'll have your SVG image file.</li>
<li>The "Preview" output box takes the same information in the source code and builds an actual SVG file into the page for you to see exactly how it will look. You may also edit the source code and click "Update" to see the preview with your changes. <em>Please note the browser compatibility list; older browsers may not support the SVG preview/editing functionality.</em></li>
</ol>
<h2>Advanced Usage Techniques</h2>
<h3>CSS Output for IE9</h3>
<p><em>(Added in 0.9.0)</em> Mark the "Generate CSS for IE9 (Base64 Output)" checkbox before clicking "Convert", and then along with the standard SVG output, you'll see another text box with base64 output. This takes the text of the SVG file and embeds it, so you can then plug it into your CSS file without the need of adding another HTTP request for an image file. <em>Note that this feature is IE9-specific. If you want to apply an SVG file as base64 to all browsers, then feel free to paste the SVG output text at <a href="http://decodebase64.com/" target="_blank">decodebase64.com</a> to get cross-browser base64 output.</em></p>
<h3 id="batch">Batch Mode</h3>
<p><em>(Added in 0.9.5)</em> Mark both the "Generate CSS for IE9 (Base64 Output)" and "Batch Mode" checkboxes, and you'll enable a special mode that lets you convert a whole bunch of gradients at once! Mark these checkboxes before adding any text input, and you'll see an example of how to use Batch Mode, show up in the input text box. Just paste your CSS selectors (containing only gradients) in the input, click "Convert", and you'll see base64 output for each selector appear in the output below. There is no preview or code updating enabled while Batch Mode is active, however.</p>
<h3>Consideration for <code>background-size</code></h3>
<p><em>(Added in 1.0.0)</em> If you use <code>background-size</code> in your CSS for custom sizing of your gradients, then include <code>background-size</code> in the script input to alter the script's behavior. The behavior change will only be apparent with input of multiple gradients; the script will make an SVG file for each individual gradient (instead of the default of one layered file for all gradients), then output cross-browser base64 (or IE9-specific if you have the relevant checkbox marked). That way, your CSS <code>background-size</code> will work as expected.</p>
<p>Why automatic base64 output, however? Because, adding HTTP requests in the form of a bunch of external SVG files reduces performance for your website visitors and therefore is not recommended. Also, if the script detects <code>background-size</code>, it will disable the preview display/update functionality, as the preview won't render properly at this time. A possible fix to re-instate that functionality may come in later releases, however.
</p>
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
<h3>Current Browser Support:</h3>
<ul>
<li><b>Full Support: </b> Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+</li>
<li><b>SVG Preview/Editing Unavailable</b>: Chrome 6-, IE8-, FF3.6-, Safari 5.0-, Opera 11.5-</li>
<li><b>Limited Support (can only do one conversion per page load/refresh):</b> FF3.6-, Opera 10-</li>
</ul>
<h3>Overview of major changes, done by Anthony Martinez:</h3>
<h4><i>Version 1.1.0</i> (June 9, 2013)</h4>
<ol>
<li>Improved error-handling, such as to catch empty input and non-pixel/non-percentage dimensions when editing the output to generate a new SVG preview.</li>
<li>Bug fix: SVG dimensions exceeding available page width would cause previews to get cropped. Now the script detects when the SVG dimensions exceed available page width, and scales the preview down accordingly (without touching your output code).</li>
<li>Bug fix: After conversion, the SVG element in the preview now has a white background, for more accurate rendering of semi-transparent or transparent gradient colors. Previously, the page's background gradient would alter the rendering of semi-transparent or transparent gradient colors.</li>
<li>Bug fix: The appearance of all monospaced text (in <code>&lt;code&gt;</code>, <code>&lt;kbd&gt;</code>, <code>&lt;input&gt;</code>, and <code>&lt;textarea&gt;</code> elements) is now standardized, correcting Opera's maverick rendering behavior. Although, to Opera's credit, the new default font of Consolas is the result of Opera's behavior.</li>
<li>Bug fix: <code>&lt;facepalm&gt;</code> Restored proper functionality to the percent and pixel radio buttons after breaking them in 1.0.0. D'oh! <code>&lt;/facepalm&gt;</code></li>
<li>Performed further tweaks to HTML and CSS to improve page usability, including adding a placeholder for the SVG preview, and removing of some unnecessary CSS.</li>
</ol>
<h4><i>Version 1.0.0</i> (June 7, 2013)</h4>
<ol>
<li>The script now detects <code>background-size</code> in input and adjusts behavior accordingly, outputting individual SVG files instead of one layered file, when multiple gradients are used. This allows for gradients to display correctly even when <code>background-size</code> is used.</li>
<li>Bug fix: When input consists of multiple gradients, and more than one of those gradients have destination or origin keywords, e.g., <code>top right</code> or <code>to bottom</code>, the script would calculate the SVG coordinates incorrectly (reusing the coords from a previous gradient). This should happen no more.</li>
<li>Bug fix: Colors defined as three-digit hex notation at a color-stop explicitly labeled 100% would get incorrectly detected as a six-digit color, e.g., <code>#RGB100</code> instead of <code>#RGB</code>. The script's regex is now updated to avoid this error.</li>
<li>Tweaked HTML and CSS to improve page usability.</li>
</ol>
<h4><i>Version 0.9.6</i> (May 28, 2013)</h4>
<ol>
<li>Improved support for IE9-. They can now generate CSS base64 output and execute Batch Mode, thanks to the tiny shim he found for the <code>window.btoa</code> function.</li>
<li>Improved error-handling in Batch Mode. If any individual gradients return an error, processing continues to the end, and those gradients that returned an error are noted in the output.</li>
<li>Improved support for IE8-, FireFox 2-, Safari 3.0-, and Opera 9.6-. They will now skip over the CSS color validation loop, thereby avoiding any errors caused by having <code>rgba</code> and/or <code>hsl/a</code> colors in the input gradient(s). Fixes issue #3 on the bottom.</li>
<li>Bug fix for IE8-: most input color names smaller than 8 letters would output a dud string in the SVG. Now the input color names get output as is, as expected.</li>
</ol>
<h4><i>Version 0.9.5</i> (May 27, 2013)</h4>
<ol>
<li>Added a Batch Mode to generate base64 CSS output for multiple selectors at once. Yes! An exclusive feature, as far as he knows. Born out of frustration with the limitations of existing LESS mixins and online gradient generators, this blows everything out of the water :) Requires <del>IE10</del> <ins>any IE</ins> or any recent release of Chrome, FF, Safari, or Opera; <del>it won't work in IE9-</del>.</li>
<li>Optimized IE9 base64 output to retain original <code>rgba</code>/<code>hsla</code>/<code>transparent</code> colors, saving a few extra bytes per stop.</li>
<li>Migrated all JS event handlers into the <code>&lt;script&gt;</code> block to separate content and behavior.</li>
</ol>
<h4><i>Version 0.9.0</i> (May 26, 2013)</h4>
<ol>
<li>Added full support for new unprefixed W3C syntax gradients (using <code>to &lt;destination&gt;</code> syntax).</li>
<li>Added logic to calculate degrees differently, to match the new W3C syntax. For example, try <code>-moz-linear-gradient(72deg,#fff,#000)</code> and <code>linear-gradient(72deg,#fff,#000)</code> in FireFox CSS &#8212; they render differently. Then input them into this script, and they should each render in SVG the same way they do in CSS.</li>
<li>If all color stop percentages are missing, then the script will now interpolate them, as happens in CSS. If only the start and ending stops are missing, the script will add them.</li>
<li>If no direction keywords or angle measurements are specified, the script will now assume defaults, as happens in CSS.</li>
<li>"Angle units"? Yeah, there's now support for all valid units, (<code>deg</code>, <code>rad</code>, <code>grad</code>, &amp; <code>turn</code>). Plus negative values and decimals work.</li>
<li>Improved support for old Webkit syntax &#8212; <code>from()</code> and <code>to()</code> will work as expected, even with decimals, and even if <code>to()</code> comes before other color-stops (as is acceptable).</li>
<li>Added support for <code>rgb/a</code> percents, <code>hsl/a</code>, floating points in <code>rgb/a</code> and <code>hsl/a</code>, <a href="http://www.w3.org/TR/SVG/types.html#ColorKeywords" title="List of valid color keywords in CSS3/SVG" target="_blank">color names</a>, and the <code>transparent</code> keyword.</li>
<li>Added logic to convert alpha values and <code>transparent</code> to proper SVG <code>stop-opacity</code> values.</li>
<li>Overhauled the SVG vector generation logic, greatly improving accuracy.</li>
<li>Added optional IE9 base64 output for CSS.</li>
<li>Added multiple background support. Yes! No other SVG or gradient generator he's aware of, even the awesome visualcsstools.com that he drew inspiration from, has this.</li>
<li>Extended SVG preview display/update capabilites to more browsers (Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+).</li>
</ol>
<h2>Known Issues</h2>
<ol>
<li>Still no radial-gradient support yet, but Anthony plans to figure that out eventually!</li>
<li>For some reason, FF3.6 and below (and Opera 10 and below) can only do one conversion per page load/refresh. Those browsers are ancient, though. So, any fixes for them will be of lowest priority for us, but you're welcome to contribute a fix! This issue is odd, though. Even IE7 can do multiple conversions! Heck, so can IE6!</li>
<li><ins>&#8212;Fixed in 0.9.6&#8212;</ins> <del>Older browsers that don't fully support <code>rgba</code> or <code>hsl/a</code> will trip on the included color validation loop, if input gradient(s) has/have <code>rgba</code> and/or <code>hsl/a</code>.</del></li>
</ol>
<h2>Road Map</h2>
<p>Anthony intends to continue updating this script as time allows. Here's what he plans to implement:</p>
<h3>Version 1.X</h3>
<ol>
<li><code>canvas</code> output support, to facilitate converting SVG output into bitmap images (e.g., PNG) that IE8- and other ancient browsers lacking SVG support can read.</li>
<li>If possible, reinstate preview functionality for when <code>background-size</code> is used.</li>
</ol>
<h3>Version 2.X</h3>
<ol>
<li>Radial gradient support.</li>
</ol>
<h2>Archived Versions</h2>
<h3><a href="http://www.kmhcreative.com/downloads/CSS2SVG/">Version 0.1</a></h3>
<p>Preview does not work in Internet Explorer, however the source code output does so you can still make SVG images with it.</p>
<p>CSS3 Gradient parameters that are <span style="color: #800000;"><strong>NOT</strong></span> supported:</p>
<ul>
<li>color stops expressed as decimals (ex. &#8220;0.7&#8243;) instead of percentages (ex. &#8220;70%&#8221;)</li>
<li>The old webkit &#8220;from&#8221; and &#8220;to&#8221; syntax is not supported. So this will not work:<br />
<em>-webkit-gradient(linear, 0% 0%, 0% 100%, from(#666666), to(#666666), color-stop(.6,#333))<br />
</em>However, the old syntax in this format IS supported:<br />
<em>background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#666666), color-stop(100%,#666666), color-stop(60%,#333333));</em></li>
<li>No support for &#8220;hsl&#8221; or &#8220;hsla&#8221; color stops. Only &#8220;hex,&#8221; &#8220;rgb&#8221; and &#8220;rgba&#8221; are supported. However &#8220;rgba&#8221; (alpha channel) support varies across browsers so you will probably want to change them to &#8220;rgb&#8221; instead for better compatibility.</li>
<li>The converter currently does not support &#8220;radial&#8221; gradients at all!</li>
</ul>
<h2>Acknowledgments</h2>
<p>Original Project Page: <a href="http://www.kmhcreative.com/labs/css3-2-svg/" target="_blank">http://www.kmhcreative.com/labs/css3-2-svg/</a></p>
<p>I&#8217;m not very good with math so I would never have been able to figure out how to build this without the following:</p>
<p><a href="http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle">http://stackoverflow.com/questions/5287954/how-to-calculate-svg-linear-gradient-attribute-x1-y1-x2-y2-if-we-know-angle</a></p>
<p><a href="http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and">http://stackoverflow.com/questions/5027950/coordinates-for-my-javascript-game-based-on-an-angle-when-do-i-use-sin-cos-and</a></p>
<p><a href="http://www.codeproject.com/KB/books/learnsvgchapter07.aspx">http://www.codeproject.com/KB/books/learnsvgchapter07.aspx</a></p>
<p>HUGE thanks to Anthony Martinez for his additions to this! <a href="http://www.linkedin.com/in/canthonymartinez/" target="_blank">http://www.linkedin.com/in/canthonymartinez/</a></p>
<h2><strong>License</strong></h2>
<p>The script is licensed under a <a href="http://creativecommons.org/licenses/by-sa/3.0/" target="_blank">Creative Commons Attribution-ShareAlike 3.0</a> license.</p>
