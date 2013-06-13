<h1>Gradient Test Cases</h1>
<p><em>By Anthony Martinez</em>
<p>If you want some gradient examples to play with in the script, then here you go!</p>
<h2>Default Mode Test Case</h2>
<p>Try this garish tri-gradient below for some fun with every allowable color-type in the script (plus errant values thrown in for extra fun), percents everywhere, and colors, colors everywhere! On top is a gratuitous semi-transparent to transparent orangish layer (just to demonstrate a non-degree unit). Then, we have a hideous looking second layer, on top of an even worse layer of all valid color names in CSS3/SVG. Who wants to calculate stops for nearly 150 colors? :P The script will do it!</p>

<pre><code>background:linear-gradient(1.79rad,rgba(255,135,15,.55),
hsla(120,0%,0%,0)),linear-gradient(66deg,palegreen,#3f5 5%,hsla(89,60%,50%,.6) 15%,
#0ed7ac 30%,transparent 35%,rgb(30%,25%,190%) 40%,rgba(37,37,22,.77) 51.5%,
pink 62.6%,hsla(415,167%,150%,.5) 68.39%,
black 75.5%,orange 87%,#123 95%,rgba(300,35,66,.5)),
linear-gradient(to bottom right,red,tan,aqua,blue,cyan,gold,gray,grey,
lime,navy,peru,pink,plum,snow,teal,azure,beige,black,brown,coral,
green,ivory,khaki,linen,olive,wheat,white,bisque,indigo,maroon,
orange,orchid,purple,salmon,sienna,silver,tomato,violet,yellow,crimson,
darkred,dimgray,dimgrey,fuchsia,hotpink,magenta,oldlace,skyblue,
thistle,cornsilk,darkblue,darkcyan,darkgray,darkgrey,deeppink,
honeydew,lavender,moccasin,seagreen,seashell,aliceblue,burlywood,
cadetblue,chocolate,darkgreen,darkkhaki,firebrick,gainsboro,goldenrod,
indianred,lawngreen,lightblue,lightcyan,lightgray,lightgrey,lightpink,limegreen,
mintcream,mistyrose,olivedrab,orangered,palegreen,peachpuff,rosybrown,
royalblue,slateblue,slategray,slategrey,steelblue,turquoise,aquamarine,
blueviolet,chartreuse,darkorange,darkorchid,darksalmon,darkviolet,
dodgerblue,ghostwhite,lightcoral,lightgreen,mediumblue,papayawhip,
powderblue,sandybrown,whitesmoke,darkmagenta,deepskyblue,floralwhite,
forestgreen,greenyellow,lightsalmon,lightyellow,navajowhite,saddlebrown,
springgreen,yellowgreen,antiquewhite,darkseagreen,lemonchiffon,
lightskyblue,mediumorchid,mediumpurple,midnightblue,darkgoldenrod,
darkslateblue,darkslategray,darkslategrey,darkturquoise,lavenderblush,
lightseagreen,palegoldenrod,paleturquoise,palevioletred,blanchedalmond,
cornflowerblue,darkolivegreen,lightslategray,lightslategrey,lightsteelblue,
mediumseagreen,mediumslateblue,mediumturquoise,mediumvioletred,
mediumaquamarine,mediumspringgreen,lightgoldenrodyellow)
</code></pre>
<p>Now try the same gradient in CSS using IE10, FF16+, Chrome 26+, or Opera 12.1+. It should look the same at the same dimensions or aspect ratio!</p>
<h2>Batch Mode Test Case</h2>
 <p>Check off both "Generate CSS for IE9 (Data URI Output)" and "Batch Mode" checkboxes while the input textarea is still empty, to reveal a sample of two selectors to test. Or, those selectors appear below. Convert them, and you should get data URI output for both of them at the same time. Powerful! The script could also make quick work of hundreds of gradients, if you were to ever have that many to have to process.</p>
<pre><code>.example1{background:linear-gradient(75deg,#fff,#000)}
.example2{background:linear-gradient(to bottom right,rgba(234,200,199,.5),#fc0,#fedcba)}</code></pre>
<h2><code>background-size</code> Test Case</h2>
<p>Paste the code below into the input, and it should produce a rainbow on top of faux window panes. Then try the gradient in CSS at the same dimensions or aspect ratio, and it should render the same!</p>
<pre><code>linear-gradient(124deg,rgba(248,248,248,.66),rgba(0,128,0,.44),rgba(0,0,128,.22)),linear-gradient(to bottom left,red,orange,yellow,green,blue,indigo,violet);background-size:25% 25%,100% 100%</code></pre>
