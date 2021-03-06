# marionette.showAnimated

Animated transition between backbone views with modified Backbone marionette.region.show()

marionette.region.showAnimated allows to use custom animations for marionette.region.show() by passing the additional parameter - animationType.
All the animation configurations code is in backbone.marionette.showAnimated.js file where any custom animation can be added. The solution is extending the original marionette.region.attachHtml() method. It doesn't affect the original marionette functionality and any existing code should be proof for any future marionette updates.

To use just include the backbone.marionette.showAnimated.js file in your project after the marionette library.

* All feedbacks are more then welcome here: https://github.com/marcinkrysiak1979/marionette.showAnimated/issues/1
* or here [![Join the chat at https://gitter.im/marcinkrysiak1979/marionette.showAnimated](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/marcinkrysiak1979/marionette.showAnimated?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# Installation

* GitHub:
  clone github repo to your desktop or download zip and attach the backbone.marionette.showAnimated.js file to your project.
* Bower: 
  bower install marionette-show-animated

# Example of use:

You can view it here: https://rawgit.com/marcinkrysiak1979/marionette.showAnimated/master/example/example.html

* THE STANDARD WAY: yourRegion.show(newView);
* THE NEW WAY: yourRegion.showAnimated(newView, {animationType: 'slideRight'});

currently I put following animation types:
* 'slideRight'
* 'slideLeft'
* 'flipRight'
* 'flipLeft'

For the animations I used TweenMax.js library - http://greensock.com/tweenmax 
so please include it as well or replace the animations with your own. I use underscore.js also but you can replace it with jquery or just pure javascript.

# Transition code example:

```
// flipLeft transition
case 'flipLeft':

  //animate out old view
  TweenMax.to(oldView.$el, 0.5, {css: {rotationY: -90}, ease: Power2.easeIn, onComplete: function() {
    
    //empty the old view
    self.el.innerHTML = ''; //from the original attachHtml method
    
    //reset the old view position
    TweenMax.set(oldView.$el, {rotationY: 0});
    
    //prepare the new view
    TweenMax.set(newView.$el, {rotationY: 90});
    
    //show the new view
    self.el.appendChild(newView.el); //from the original attachHtml method
    
    //animate in the new view
    TweenMax.to(newView.$el, 0.5, {rotationY: 0, ease: Power2.easeOut});
    
  }});
break;
```
