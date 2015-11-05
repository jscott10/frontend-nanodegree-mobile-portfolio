## Website Performance Optimization portfolio project

### Objective 1: Achieve 90+ score on PageSpeed Insights (mobile and desktop) on index.html:

#### Optimizations

1. Changes to `index.html`
 * Move the inline Google Analytics function to the bottom of the page
 * Add async attribute to the `analytics.js` link
 * Use inline javascript to reference the Google Font
 * Make the css from `style.css` inline
 * Specify `"media='print'"` for `print.css` link
 * Create `smartphone-style.css` containing the smartphone media querie section of style.css, reference using media query from `index.html`
2. Images
 * Store local copies of the external images
 * Resize the `pizzeria.jpg` image to 100px (per inline style)
3. Optmizations
 * Optimize images (`grunt-contrib-imagemin`)
 * Minify javascript (`grunt-contrib-uglify`)
 * Minify css (`grunt-contrib-cssmin`)
 * Minify html (`grunt-contrib-htmlmin`)

Pagespeed: **93** mobile / **95** Desktop

### Objective 2: Achieve 60fms scrolling on pizza.html

#### Optimizations

Issue: function updatePositions() references document.body.scrollTop for each pizza image on every scroll event. Reflow occurs every time scrollTop is read.
Fix: refactor updatePositions() to move the reference to document.body.scrollTop outside the for loop.
Result: Page scrolls at 60fms.

### Objective 3: Achieve <5ms pizza resizing on pizza.html

#### Optimizations

1. functions function determineDx(elem, size) and changePizzaSizes(size) both reference the offsetWidth of each randomPizzaContainer element. Reflow occurs every time offsetWidth is read.
2. determineDx(elem, size) references the offsetWidth of #randomPizzas. Reflow occurs every time offsetWidth is read.
3. document.querySelectorAll(".randomPizzaContainer") is called as the for-loop limit and in the body of the for loop

Fix:	1 and 2: refactor determineDx(elem, size) as determineDx(windowwidth, elemOffsetWidth, size) and store randomPizzaContainer.offsetWidth and randomPizzas.offsetWidth once at the beginning of the function.
	3: Store the array of randomPizzaContainers at the beginning of the function.

Pizza resizing occurs in **~0.4ms**

