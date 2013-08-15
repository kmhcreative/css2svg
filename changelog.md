<h1>Changelog for Previous & Archived Releases</h1>
<p><em>By Anthony Martinez</em></p>
<h2>Previous Releases</h2>
<h3><i>Version 1.2.0</i> (June 12, 2013)</h3>
<ol>
<li>Support for SVG output as base64 is now dropped in favor of partially encoded ASCII, which is more efficient than base64 and is at least somewhat legible, too. Credit for inspiration goes to this <a href="http://coding.smashingmagazine.com/?p=126525">clever article he read on Smashing Magazine</a>, showing him for the first time that data URIs don't always have to be in base64.</li>
<li>Preview display is now available when using <code>background-size</code> in input. There is and will likely not be any support for editing/updating the output, however. Instead, to make changes, edit your original input and convert again.</li>
<li>The output boxes and preview get cleared or reset upon toggling Batch Mode.</li>
<li>Firefox 3.6-, Opera 10-, and perhaps a few other older browsers now have support for performing multiple conversions. Fixes issue #2 on the bottom. It was an old regex parsing quirk, fixed by just adding one line: <code>token.lastIndex=0</code>. Don't you love easy fixes?</li>
<li>Bug fix: Using <code>background-size</code> in Batch Mode input led to awful errors in output.</li>
<li>Bug fix: The script did not previously allow for decimal angle measurements lacking at least one leading digit. For example: <code>0.5deg</code> would work, but not <code>.5deg</code>.</li>
<li>Bug fix: When doing multiple conversions of varying dimensions (including any that exceed available page width and therefore get scaled down to fit the page), the preview may display at an incorrect aspect ratio.</li>
<li>Bug fix / improvement in error-handling: The SVG output text box and Update button should not activate after a failed conversion.</li>
<li>Bug fix / improvement in error-handling: The error message for use of the non-standard <code>center</code> keyword in input was not always being thrown properly.</li>
<li>The script now complies with <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode">ECMAScript 5's Strict Mode</a>.</li>
<li>Further tweaks to the page to improve usability, including adding <code>label</code> elements, making input element text now clickable (not just the radio buttons or checkboxes themselves).</li>
<li>The CSS component is now slimmed down by a further 20%, thanks to the removal of unneeded code and optimization of the remaining code. Now, if getting the size of the JS component under control were only as simple... Actually, despite all the changes in this release, the JS is about 5% smaller compared to 1.1.0, but that could be attributed mostly to the migration of the mammoth test case out of the script and into a separate file (<a href="https://github.com/camartinez1229/css2svg/blob/master/gradient-test-cases.md">test case file</a>) for better discoverability. Ignoring that removal, the JS actually saw a 5% gain in file size.</li>
</ol>
<h3><i>Version 1.1.0</i> (June 9, 2013)</h3>
<ol>
<li>Improved error-handling, such as to catch empty input and non-pixel/non-percentage dimensions when editing the output to generate a new SVG preview.</li>
<li>Bug fix: SVG dimensions exceeding available page width would cause previews to get cropped. Now the script detects when the SVG dimensions exceed available page width, and scales the preview down accordingly (without touching your output code).</li>
<li>Bug fix: After conversion, the SVG element in the preview now has a white background, for more accurate rendering of semi-transparent or transparent gradient colors. Previously, the page's background gradient would alter the rendering of semi-transparent or transparent gradient colors.</li>
<li>Bug fix: The appearance of all monospaced text (in <code>&lt;code&gt;</code>, <code>&lt;kbd&gt;</code>, <code>&lt;input&gt;</code>, and <code>&lt;textarea&gt;</code> elements) is now standardized, correcting Opera's maverick rendering behavior. Although, to Opera's credit, the new default font of Consolas is the result of Opera's behavior.</li>
<li>Bug fix: <code>&lt;facepalm&gt;</code> Restored proper functionality to the percent and pixel radio buttons after breaking them in 1.0.0. D'oh! <code>&lt;/facepalm&gt;</code></li>
<li>Performed further tweaks to HTML and CSS to improve page usability, including adding a placeholder for the SVG preview, and removing of some unnecessary CSS.</li>
</ol>
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
