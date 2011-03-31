
==Introduction==

I wrote a JQuery add-on that can be used to remove CSS from elements. I place the code hare, so it could help.

==The JQuery add-on==

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
          cssClearAttr = cssClearAttr.replace(/^\[/, '');
          cssClearAttr = cssClearAttr.replace(/\]$/, '');
          
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
