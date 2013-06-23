<h1>Changelog for Previous & Archived Releases</h1>
<p><em>By Anthony Martinez</em></p>
<h2>Previous Releases</h2>
<h3><i>Version 1.0.0</i> (June 7, 2013)</h3>
<ol>
<li>The script now detects <code>background-size</code> in input and adjusts behavior accordingly, outputting individual SVG files instead of one layered file, when multiple gradients are used. This allows for gradients to display correctly even when <code>background-size</code> is used.</li>
<li>Bug fix: When input consists of multiple gradients, and more than one of those gradients have destination or origin keywords, e.g., <code>top right</code> or <code>to bottom</code>, the script would calculate the SVG coordinates incorrectly (reusing the coords from a previous gradient). This should happen no more.</li>
<li>Bug fix: Colors defined as three-digit hex notation at a color-stop explicitly labeled 100% would get incorrectly detected as a six-digit color, e.g., <code>#RGB100</code> instead of <code>#RGB</code>. The script's regex is now updated to avoid this error.</li>
<li>Tweaked HTML and CSS to improve page usability.</li>
</ol>
<h3><i>Version 0.9.6</i> (May 28, 2013)</h3>
<ol>
<li>Improved support for IE9-. They can now generate CSS base64 output and execute Batch Mode, thanks to the tiny shim he found for the <code>window.btoa</code> function.</li>
<li>Improved error-handling in Batch Mode. If any individual gradients return an error, processing continues to the end, and those gradients that returned an error are noted in the output.</li>
<li>Improved support for IE8-, FireFox 2-, Safari 3.0-, and Opera 9.6-. They will now skip over the CSS color validation loop, thereby avoiding any errors caused by having <code>rgba</code> and/or <code>hsl/a</code> colors in the input gradient(s). Fixes issue #3 on the bottom of the README.</li>
<li>Bug fix for IE8-: most input color names smaller than 8 letters would output a dud string in the SVG. Now the input color names get output as is, as expected.</li>
</ol>
<h3><i>Version 0.9.5</i> (May 27, 2013)</h3>
<ol>
<li>Added a Batch Mode to generate base64 CSS output for multiple selectors at once. Yes! An exclusive feature, as far as he knows. Born out of frustration with the limitations of existing LESS mixins and online gradient generators, this blows everything out of the water :) Requires <del>IE10</del> <ins>any IE</ins> or any recent release of Chrome, FF, Safari, or Opera; <del>it won't work in IE9-</del>.</li>
<li>Optimized IE9 base64 output to retain original <code>rgba</code>/<code>hsla</code>/<code>transparent</code> colors, saving a few extra bytes per stop.</li>
<li>Migrated all JS event handlers into the <code>&lt;script&gt;</code> block to separate content and behavior.</li>
</ol>
<h3><i>Version 0.9.0</i> (May 26, 2013)</h3>
<ol>
<li>Added full support for new unprefixed W3C syntax gradients (using <code>to &lt;destination&gt;</code> syntax).</li>
<li>Added logic to calculate degrees differently, to match the new W3C syntax. For example, try <code>-moz-linear-gradient(72deg,#fff,#000)</code> and <code>linear-gradient(72deg,#fff,#000)</code> in FireFox CSS &#8212; they render differently. Then input them into this script, and they should each render in SVG the same way they do in CSS.</li>
<li>If all color stop percentages are missing, then the script will now interpolate them, as happens in CSS. If only the start and ending stops are missing, the script will add them.</li>
<li>If no direction keywords or angle measurements are specified, the script will now assume defaults, as happens in CSS.</li>
<li>"Angle units"? Yeah, there's now support for all valid units, (<code>deg</code>, <code>rad</code>, <code>grad</code>, &amp; <code>turn</code>). Plus negative values and decimals work.</li>
<li>Improved support for old WebKit syntax &#8212; <code>from()</code> and <code>to()</code> will work as expected, even with decimals, and even if <code>to()</code> comes before other color-stops (as is acceptable).</li>
<li>Added support for <code>rgb/a</code> percents, <code>hsl/a</code>, floating points in <code>rgb/a</code> and <code>hsl/a</code>, <a href="http://www.w3.org/TR/SVG/types.html#ColorKeywords" title="List of valid color keywords in CSS3/SVG" target="_blank">color names</a>, and the <code>transparent</code> keyword.</li>
<li>Added logic to convert alpha values and <code>transparent</code> to proper SVG <code>stop-opacity</code> values.</li>
<li>Overhauled the SVG vector generation logic, greatly improving accuracy.</li>
<li>Added optional IE9 base64 output for CSS.</li>
<li>Added multiple background support. Yes! No other SVG or gradient generator he's aware of, even the awesome visualcsstools.com that he drew inspiration from, has this.</li>
<li>Extended SVG preview display/update capabilites to more browsers (Chrome 7+, IE9+, FF4+, Safari 5.1+, Opera 11.6+).</li>
</ol>
<h2>Archived Versions by KMH Creative</h2>
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
