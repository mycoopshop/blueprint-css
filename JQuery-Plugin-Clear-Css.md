## DRAFT
Please note that this page currently is in draf mode. Don't use this on any live site until this message is gone. If you got any ideas or additions, feel free to go and share your thoughts on our google mailing list. Thank you.
## Introduction

For some reason, I wanted to remove CSS from an element, and from all its children. So I wrote a JQuery add-on that can be used to remove CSS from an element, and from all its children.

You can remove: Only the classes, only the in-line styles. only a given list of properties, or any combination of the 3 actions above.

Note : To get the list of CSS properties from a given set of style sheets, see the Perl script [[property-extractor]].

Original Thread: [[http://groups.google.com/group/blueprintcss/browse_thread/thread/92fdc90621a12a94?hl=de]]

## The JQuery add-on

We assume that the JavaScript file is "cssClear.js".


       /**
        * This add-on removes CSS for a given element, and for **all its children**.
        * The following CSS can be removed:
        *   o Only a given list of properties (given as an array).
        *   o Only the classes.
        *   o Only the in-line style definition.
        *   o Or any combination of the 3 previous actions.
        *
        * @autor Denis BEURIVE
        * @example
        *   <script type="text/javascript" src="jquery-1.4.4.min.js"></script>
        *   <script type="text/javascript" src="cssClear.js"></script>
        *   <script language="javascript">
        *       $(function()
        *       {
        *           var cssProperties = new Array('font-style','border-right-width','background','padding-right','border','margin','border-right','height','margin-top','border-left-width','margin-right','color','width','position','display','padding-left','float','border-width','content','overflow-x','margin-left','border-bottom','border-color','border-style','background-color','font-family','padding','font','visibility','overflow','white-space','line-height','padding-top','margin-bottom','border-collapse','text-align','border-spacing','font-size','font-weight','clear','text-decoration','vertical-align');
        *           var otheCssProperties = new Array('font-style','border-right-width');
        *           $('[cssCleaning]').cssClear(cssProperties);
        *           $('[otherCssCleaning]').cssClear(otheCssProperties);
        *       });
        *   </script>
        *   ...
        *   <!-- Remove everything (properties, classes and in-line styles). -->
        *   <div cssCleaning="properties|classes|styles" class="span-20" style="background-color:#c0c0c0">...</div>
        *   <!-- Remove only properties and classes. -->
        *   <div cssCleaning="properties|classes" class="span-20" style="background-color:#c0c0c0">...</div>
        *   <!-- Remove only properties. -->
        *   <div otherCssCleaning="properties" class="span-20" style="background-color:#c0c0c0">...</div>
        */
        
       (function($)
       {
           /**
            * This function removes a given list of CSS properties from an element.
            * @param inElement The element.
            * @param inCssProperties Array that contains the list of CSS properties to remove.
            */
       
           function removeAllProperties (inElement, inCssProperties)
           {
               for (k=0; k<inCssProperties.length; k++)
               {
                   var p = inCssProperties[k];
                   inElement.css(p, '').find('*').css(p, '');
               }
           }
           
           /**
            * This function removes CSS from a given element.
            * @param inCssProperties Array that contains the list of properties to remove.
            * @inOptions Options (this argument is not used right now).
            */
           
           $.fn.cssClear = function(inCssProperties, inOptions)
           {
               // Are there options?
               var options = (typeof inOptions == 'undefined') ? new Array() : inOptions;
               
               // Do we have a list of properties?
               inCssProperties = (typeof inCssProperties == 'undefined') ? new Array() : inCssProperties;
               
               // If there is no selected element, then abort.
               if (0 == $(this).length) { return; }
       
               // Which attribute represents selector?
               var cssClearAttr = this.selector;
               
               // Remove the first and the last character.
               cssClearAttr = cssClearAttr.substring(0, cssClearAttr.length - 1);
               cssClearAttr = cssClearAttr.substring(1, cssClearAttr.length);
               
               // Create all elements returned by the JQuery's selector.
               for (i=0; i<$(this).length; i++)
               {
                   var element = $(this).eq(i);
                   var todo    = element.attr(cssClearAttr);
                   var actions = todo.split('|');
                   
                   for (j=0; j<actions.length; j++)
                   {
                       switch (actions[j])
                       {
                           case 'properties': removeAllProperties(element, inCssProperties); break;
                           case 'classes':    element.removeClass().find('*').removeClass(); break;
                           case 'styles':     element.attr('style', '').find('*').element.attr('style', ''); break;
                           default: alert('cssClear: Invalid action' + actions[j] + '!');
                       }
                   }
               }
           }
       })( jQuery );

## How to use it?

Include JQuery:

    <script type="text/javascript" src="jquery-1.4.4.min.js"></script>

Include the add-on:

    <script type="text/javascript" src="cssClear.js"></script>

Call the add-on on a set of elements: Elements are designed by an attribute. Here, we use 2 distinct attributs: "cssCleaning" and "otherCssCleaning". All elements that present these attributs will be processed by the add-on.

    <script language="javascript">
        $(function()
        {
            var cssProperties = new Array('font-style','border-right-width',...);
            var otheCssProperties = new Array('font-style','border-right-width');
            $('[cssCleaning]').cssClear(cssProperties);
            $('[otherCssCleaning]').cssClear(otheCssProperties);
        });
    </script>

Note: This code calls the add-on once the DOM is fully loaded (see JQuery documentaiton). You can call this add-on later if you need.

In your HTML code, define the elements that will be "CSS cleared".

        <!-- Remove everything (properties, classes and in-line styles). -->
        <div cssCleaning="properties|classes|styles" class="span-20" style="background-color:#c0c0c0">...</div>

        <!-- Remove only properties and classes. -->
        <div cssCleaning="properties|classes" class="span-20" style="background-color:#c0c0c0">...</div>

        <!-- Remove only properties. -->
        <div otherCssCleaning="properties" class="span-20" style="background-color:#c0c0c0">...</div>

