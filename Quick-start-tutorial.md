Welcome to this tutorial on Blueprint. It will give you a thorough intro to what you can do with the framework, and a few notes on what you shouldn’t do with it. Let’s get started.

About Blueprint
---------------
Blueprint is a CSS framework, designed to cut down on your development time. It gives you a solid foundation to build your CSS on top of, including some sensible default typography, a customizable grid, a print stylesheet and much more.

However, BP is not a silver bullet, and it’s best suited for websites where each page may require its own design. Take a look at existing BP pages before deciding if the framework is right for you. You may also check out the test files in the tests directory, which demonstrates most of the features in Blueprint.

The word “framework” may be a bit misleading in this context, since BP does not make suggestions on how you should organize or write your CSS. It’s more like a “css toolbox” with helpful bits and pieces, from which you may pick and choose based on your needs.

Structural Overview
-------------------
From the bottom up, here are the CSS layers in Blueprint:

*	CSS reset: Removes any default CSS rules set by each browser.
*	Typography: Gives you some nice default typography and colors.
*	Grid: Provides a set of CSS classes for making grid layouts.

The second part of Blueprint are the scripts, which let you customize most
aspects of the framework, from column count and widths, to output paths and
CSS class namespaces. We have two scripts:

Compressor: For compressing and customizing the source files.  
Validator: For validating the Blueprint core files.  
That’s the quick overview, so now we can finally get into the details. First, we’ll take 
a look at the CSS in Blueprint. We’ll then move on to the scripts, where I’ll show you 
how to customize the framework.

Setting Up Blueprint
To use Blueprint, you must include three files in your HTML:

blueprint/screen.css:	All CSS for screen, projection viewing.
blueprint/print.css: A basic stylesheet for printing.
blueprint/ie.css:	A few needed corrections for Internet Explorer
To include them, use the following HTML (make sure the href paths are correct):


    <link rel="stylesheet" href="css/blueprint/screen.css" type="text/css" media="screen, projection">
    <link rel="stylesheet" href="css/blueprint/print.css" type="text/css" media="print"> 
    <!--[if lt IE 8]>
      <link rel="stylesheet" href="css/blueprint/ie.css" type="text/css" media="screen, projection">
    <![endif]-->

Remember to add trailing slashes if you’re using XHTML (" />").

Using the CSS in Blueprint
--------------------------
As mentioned before, there’s basically three layers of CSS in Blueprint. The first two layers, the browser CSS reset and the default typography, apply themselves by changing the CSS of standard HTML elements. In other words, you don’t need to change anything in these files. If you, for instance, want to change the font size, do this in your own stylesheet, so that it’s easy to upgrade Blueprint when new versions arrive.

Classes for Typography
----------------------
While the typography of Blueprint mainly applies itself, there’s a few classes
provided. Here’s a list of their names and what they do:

`.small` Makes the text of this element smaller.  
`.large` Makes the text of this element larger.  
`.hide` Hides an element.  
`.quiet` Tones down the font color for this element.  
`.loud` Makes this elements text black.  
`.highlight` Adds a yellow background to the text.  
`.added` Adds green background to the text.  
`.removed` Adds red background to the text.  
`.first` Removes any left sided margin/padding from the element.  
`.last` Removes any right sided margin/padding from the element.  
`.top` Removes any top margin/padding from the element.  
`.bottom` Removes any bottom margin/padding from the element.  

Styling Forms
-------------

To make Blueprint style your input elements, each text input element should
have the class .text, or .title, where .text is the normal size,
and .title gives you an input field with larger text.

There’s also a few classes you may use for success and error messages:

div.error  
Creates an error box (red).  
div.notice  
Creates a box for notices (yellow).  
div.success  
Creates a box for success messages (green).  

Creating a Grid
---------------

The third layer is the grid CSS classes, which is the tool Blueprint gives you to create almost any kind of grid layout for your site. Keep in mind that most of the CSS behind the grid can be customized (explained below). In this section however, I’m using the default settings.

The default grid is made up of 24 columns, each spanning 30px, with a 10px margin between each column. The total width comes to 950px, which is a good width for 1024×768 resolution displays. If you’re interested in a narrower design, see the section on customizing the grid, below.

So how do you set up a grid? By using classes provided by Blueprint. To create a column, make a new `<div/>`, and apply one of the .span-x classes to it. For instance, if you want a 3-column setup, with two narrow and one wide column, a header and a footer here’s how you do it:
			
    <div class="container">
  	<div class="span-24">
  		The header
  	</div>

  	<div class="span-4">
  		The first column
  	</div>
  	<div class="span-16">
  		The center column
  	</div>
  	<div class="span-4 last">
  		The last column
  	</div>
	
  	<div class="span-24">
  		The footer
  	</div>
    </div>

In addition to the spans, there are two important classes you need to know about. First of all, every Blueprint site needs to be wrapped in a div with the class .container, which is usually placed right after the body tag.

Second, the last column in a row (which by default has 24 columns), needs the class .last to remove its right hand margin. Note, however, that each .span-24 does not need the .last class, since these always span the entire width of the page.

To create basic grids, this is all you need to know. The grid CSS however, provides many more classes for more intricate designs. To see some of them in action, check out the files in tests/parts/. These files demonstrate what’s possible with the grid in Blueprint.

Here’s a quick overview of the other classes you can use in to make your grid:

.append-x  
Appends x number of empty columns after a column.  
.prepend-x  
Prepends x number of empty columns before a column.  
.push-x  
Pushes a column x columns to the left. Can be used to swap columns.  
.pull-x  
Pulls a column x columns to the right. Can be used to swap columns.  
.border  
Applies a border to the right side of the column.  
.colborder  
Appends one empty column, with a border down the middle.  
.clear  
Makes a column drop below a row, regardless of space.  
.showgrid  

Add to container or column to see the grid and baseline.  
In this list, x is a number from 1 through 23 for append/prepend and 1 through 24 for push/pull. These numbers will of course change if you set a new number of columns in the settings file.  

Here’s another example where we have four columns of equal width, with a border between the two first and the two last columns, as well as a four column gap in the middle:

				
	<div class="container">
		<div class="span-5 border">
			The first column
		</div>
		<div class="span-5 append-4">
			The second column
		</div>
		<div class="span-5 border">
			The third column
		</div>
		<div class="span-5 last">
			The fourth (last) column
		</div>
	</div>

You may also nest columns to achieve the desired layout. Here’s a setup where we want four rectangles with two on top and two below on the first half of the page, and one single column spanning the second half of the page:

				
	<div class="container">
		<div class="span-12">
			<div class="span-6">
				Top left
			</div>
			<div class="span-6 last">
				Top right
			</div>
			<div class="span-6">
				Bottom left
			</div>
			<div class="span-6 last">
				Bottom right
			</div>
		</div>
		<div class="span-12 last">
			Second half of page
		</div>
	</div>

Try this code in your browser if it is difficult to understand what it would look like. To see more examples on how to use these classes, check out /tests/parts/grid.html.

The Scripts
-----------
Blueprint comes with two scripts: one for compressing and customizing the CSS, and one for validating the core CSS files, which is handy if you’re making changes to these files.

The Validator
-------------
The validator has a fairly simple job – validate the CSS in the core BP files. The script uses a bundled version of the W3C CSS validator to accomplish this. To run it, you’ll need to have Ruby installed on your machine. You can then run the script like so: $ ruby validate.rb.

Note that there are a few validation errors shipping with Blueprint. These are known, and comes from a few CSS hacks needed to ensure consistent rendering across the vast browser field.

The Compressor
--------------
As the files you’ll include in your HTML are the compressed versions of the core CSS files, you’ll have to recompress the core if you’ve made any changes. This is what the compressor script is for.

In addition this is where you customize the grid. To customize the grid, a special settings file is used, and the new CSS is generated once you run the compressor. The new compressed files will then reflect your settings file.

To recompress, you just have to run the script. This will parse the core CSS files and output new compressed files in the blueprint folder. As with the validator, Ruby has to be installed to use this script. In the lib directory, run: $ruby compress.rb

Calling this file by itself will pull files from blueprint/src and concatenate them into three files; ie.css, print.css, and screen.css. However, argument variables can be set to change how this works. Calling $ruby compress.rb -h will reveal basic arguments you can pass to the script.

Custom Settings
---------------

To learn how to use custom settings, read through the documentation within lib/compress.rb