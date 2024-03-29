# DRAFT
Please be aware that the code shown on this page currently is only draft. Please don't use this on any production or live site unless this message is gone.

# Introduction

This page shows how to create rounded corners and rounded borders with BluePrint and JQuery.

The rounding is done by the pretty good JQuery add-on "JQuery Corner" : [[http://jquery.malsup.com/corner/]]

# How to use it

Load JQuery:
    <script type="text/javascript" src="jquery-1.4.4.min.js"></script>

Load JQuery Corner add-on:
    <script type="text/javascript" src="jquery.corner.js"></script>

Call the add-on on the element you want to round:
    <script language="javascript">
        $(function()
        {
            $("[box]").corner("10px");
            $('div.inner').corner("round 8px");
            $('div.outer').corner("10px");
        });
    </script>

# Full example

Copy/Paste the following HTML code to a file (say "test.html"). Then load the file into your browser.

Make sure to put the JQuery library (jquery-1.4.4.min.js) in the same directory.

Make sure to put the JQuery add-on (jquery.corner.js) in the same directory.

My CSS definitions may be really bad... I am not good at CSS ;-)




        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"><html xmlns="http://www.w3.org/1999/xhtml">
        
        <head>
            <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        	
            <!-- Chargement des feuilles de style BluePrint. -->
            <link rel="stylesheet" href="blueprint/screen.css" type="text/css" media="screen, projection">
            <link rel="stylesheet" href="blueprint/print.css" type="text/css" media="print">
            <!--[if lt IE 8]><link rel="stylesheet" href="blueprint/ie.css" type="text/css" media="screen, projection"><![endif]-->
            
            <!-- Chargement des librairies JavaScript. -->
            <script type="text/javascript" src="jquery-1.4.4.min.js"></script>
            <script type="text/javascript" src="jquery.corner.js"></script>
            
            <script language="javascript">
                $(function()
                {
                    // We create rounded corners for all divisions that have the attribute "box".
                    $("[box]").corner("10px");
                    $('div.inner').corner("round 8px");
                    $('div.outer').corner("10px");
                });
            </script>
                
            <style type="text/css"> 
                
                .padding10 { padding:10px; }
                
                .padding11 { padding:11px; }
            
                .padding15 { padding:15px; }
                
                .padding20 { padding:20px; }
        		
        		.padding30 {  padding-left: 30px; padding-right: 30px; }
                
                .border1 { border-width:1px; border-style:solid; border-color:#000000; }
                
                .bigdiv { width:920px; }
            
                .gradient   {
                                background-image: url("sectionLrgBack.jpg");
                                background-repeat: no-repeat;
                                color: #000000;
                                width: 100%;
                                text-align: left;
                           }
                           
                .green  { background-color:#BDFFB2; }
                        
                .blue   { background-color:#B2E3FF; }
                        
                .orange { background-color:#FFAE80; }
        
                div.outer {
                            float:left;
                            background: #c82;
                            padding-left:5px;
                            padding-right:5px;
                            padding-top:5px;
                            padding-bottom:5px;
                            width:940px;
                          }
                
                div.inner {
                            padding-top: 10px;
                            padding-bottom: 10px;
                            margin-left:5px;
                          }
        		
            </style>
            
        </head>
        <body>
            
            <div class="container">
        
                <div class="span-24 last">
                    <p>This page shows how to add rounded corners with BluePrint and JQuery.</p>
                    <ul>
                        <li>BluePrint: http://blueprintcss.org</li>
                        <li>JQuery: http://jquery.com/</li>
                        <li>JQuery plugin for rounded corners: http://jquery.malsup.com/corner/</li>
                    </ul>
                </div>
            
        		<hr class="space"/>
                <h2>Using JQuery to create rounded corners.</h2>
            
                <div box="yes" class="orange bigdiv padding15 large clear">
                    This is not a "BluePrint division".<br/>
                    Total width = width + padding-right + padding-left = 920+15+15 = 950px.<br/>
                    Please note the use of the class "clear": The current division will place itself underneath all divisions previously declared in the document.
                </div>
                
                <hr class="space"/>
                
                <!-- Usage 1 -->
                <div class="span-12">
                    <div box="yes" class="green padding15 large">BluePrint left (span-12)</div>
                </div>
                <div class="span-12 last">
                     <div box="yes" class="blue padding15 large">BluePrint right (span-12)</div>
                </div>
            
                <hr class="space"/>
         
                <div box="yes" class="orange padding20 span-23">
                
                    <ul>
                        <li>padding-left=20px</li>
                        <li>padding-right=20px</li>
                        <li>nomimal width=910px (span-23)</li>
                        <li>total width=910+20+20=950px</li>
                    </ul>
                    
                    <p>And:</p>
                    
                    <ul>
                        <li>Gap between the 2 inner BluePrint divisions (the green and the blue): 10px</li>
                        <li>Width of the green BluePrint division: 450px.</li>
                        <li>Width of the blue BluePrint division: 450px.</li>
                        <li>Total width: 450 + 450 + 10 = 910px (that is: The size of the main container - span-23)</li>
                    </ul>
                
                    <div box="yes" class="span-11 padding10 green">
                        BluePrint left division.
                        <ul>
                            <li>padding-left=10px</li>
                            <li>padding-right=10px</li>
                            <li>nomimal width=430px (span-11)</li>
                            <li>total width=430+10+10=450px</li>
                        </ul>
                    </div>
                    
                    <div box="yes" class="span-11 padding10 blue last">
                        BluePrint right division.
                        <ul>
                            <li>padding-left=10px</li>
                            <li>padding-right=10px</li>
                            <li>nomimal width=430px (span-11)</li>
                            <li>total width=430+10+10=450px</li>
                        </ul>
                    </div>    
                </div>
                
        		<hr class="space"/>
        		
                <h2>Using JQuery to create rounded borders.</h2>
        		
                <div class="outer">
                    <div class="inner span-22 padding30 orange">
                        <ul>
                            <li>Total width for the inner division = span-22 + paddin-left + padding-right = 870 + 30 + 30 = 935px</li>
        					<li>Position of the left border for the inner division: marging-left + total width = 5 + 935 = 940px</li>
                            <li>Trick! BluePrint's class "span-22" defines a right margin of 10px. But, there is nothing to the right of the division. Therefore, this space is not included in the calcul of the total width.</li>
                            <li>Total width for the outer division = 940 + padding-left + padding-right = 950px.</li>
                        </ul>
                    </div>
                </div>
            
                <hr class="space"/>
            
            </div> <!-- .container -->
        </body>
        </html>



OK


!






