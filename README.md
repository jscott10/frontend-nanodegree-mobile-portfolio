## Website Performance Optimization portfolio project

### Objective 1: Achieve 90+ score on PageSpeed Insights (mobile and desktop) on index.html:

#### Optimizations

1. Changes to index.html
* Move the inline Google Analytics function to the bottom of the page
* Add async attribute to the analytics.js link
* Use inline javascript to reference the Google Font
* Make the css from style.css inline
* Specify "media='print'" for print.css link
* Create smartphone-style.css containing the smartphone media querie section of style.css, reference using media query from index.html
2. Images
* Store local copies of the external images
* Resize the pizzeria.jpg image to 100px (per inline style)
3. Optmizations
* Optimize images (grunt-contrib-imagemin)
* Minify javascript (grunt-contrib-uglify)
* Minify css (grunt-contrib-cssmin)
* Minify html (grunt-contrib-htmlmin)

Pagespeed: **93** mobile / **95** Desktop

### Objective 2: Achieve 60fms scrolling on pizza.html

#### Optimizations

*updatePositions():*

* Refactor document.body.scrollTop out of the for loop (line 527) to eliminate forced synchronous layout.
* Replace querySelectorAll(".mover") with getElementsByClassName("mover") (line 529), the latter executes faster.
* Specify pizza image locations using tranform instead of left (line 535). Left triggers layout and paint, transform only trigger composite.
* translate3d(x,y,z) is faster than translateX(x) because translate3d(x,y,z) forces the composite operation onto the GPU (http://stackoverflow.com/questions/22111256/translate3d-vs-translate-performance)

*addEventListener("scroll", updatePositions):*

* Added code to calculate initial positions (lines 574-576).
* Added code to calculate the number of visible pizza rows (lines 562-565)

Page scrolls at 60fms.

### Objective 3: Achieve <5ms pizza resizing on pizza.html

#### Optimizations

* Eliminate determineDx(elem, size), factoring out sizeSwitcher(size). (line 457)
* Change sizeSwitcher to return a percentage value
* Refactor to move document.querySelectorAll(".randomPizzaContainer") out of the for loop. (line 474)
* Replace querySelectorAll(".randomPizzaContainer") with getElementsByClassName("randomPizzaContainer") (line 474), the latter executes faster.
* Set randomPizzaContainers[x].style.width to a percentage value.

Pizza resizing occurs in **~0.4ms**

