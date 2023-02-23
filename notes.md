REVIEW
Padding: section between content box and border

1. left
2. right
3. top
4. bottom
5. all sides

Margin: spacing on the outside of a border

Display property:

- block: element takes the whole line width
- inline: elemments fit along side eachother on the same line
- inline-block: an inline element except WIDTH, HEIGHT, MARGIN & PADDING are respected

Percentage is relative to another property
percentages are popular with width and height

With font size 1em is equal to the computed font-size of the parent
With other properties 1em is equal to the computed font size of the element itself

Position:

# Section 2

## 6. Building the Header - Part 1

1. The best way to perform a bsic rest using the universal selector
2. How to set project wide font definitions
3. How to clip parts of elements using clip path

universal selector:
start clean
set box properties, change box model so border and padding no longer added to total width/height of element

font properties in the body selector, using inheritance so all child selectors inherit the properties.

clippy - online tool you choose the shape and it gives you the polygon shape

style.css

```
/* Basic Reset */
/* universal selector, start clean*/
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* font properties, padding gives the white border around the page */
body {
  font-family: "Lato", sans-serif;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.7;
  color: #777;
  /* white border around the webpage */
  padding: 30px;
}

/* cover: try to fit the element in the box */
.header {
  height: 95vh;
  /* gradient to right bottom, 2 images: linear grad, url(../) */
  background-image: linear-gradient(
      to right bottom,
      rgba(126, 213, 111, 0.8),
      rgba(40, 180, 133, 0.8)
    ),
    url(../img/hero.jpg);

  background-size: cover;
  background-position: top;
  /* define coordinates of a polygon, starting left top, and then define each corner going clockwise */
  /* Triangle */
  /* clip-path: polygon(50% 0, 100% 100%, 0 100%, 0 100%); */

  /* vh set the height dynamic to viewport height */
  clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
  /* clip-path: polygon(x y, x y, x y); */
}
```

## 7. Building the Header - Part 2

center items
add image

index.html

```
  <header class="header">
      <div class="logo-box">
        <img src="img/logo-white.png" alt="Logo" class="logo" />
      </div>

      <!-- 7. use span 2 font size in a single h1 (seo) -->
      <h1 class="heading-primary">
        <span class="heading-primary-main">Outdoors</span>
        <span class="heading-primary-sub">is where life happens</span>
      </h1>
    </header>


```

style classes
display elements one on top of the other,
added position relative to .header so logo-box has a reference.
use block elements: they occupy whole width and they create line break before and after the element
position element in middle always, responsive
positon classes in natural order of HTML (organizational)

Sebastian explains transform:
While the first piece of code positions the element 50% from the top and 50% from the left of its container, its does so while considering the start or origin point of the element to be its top-left corner.

This results in it not being quite centered; only its top-left corner (if I remember well) is centered, while what we want is the very center of the element to be centered.

This is achieved by the second piece of code, which moves the element 50% away from its own left and 50% away from its own top, thus making the element truly centered within its container together with the former piece of code.

The transform ought to work with inline-block and block elements (so not paragraph text), since they have such possibilities of positioning, whereas inline elements do not.

.css

```
/* 7. Icon logo*/
.logo-box {
  position: absolute;
  top: 40px;
  left: 40px;
}

.logo {
  height: 35px;
}

/* Centering header. text box top and left in relation to parent el, translate in relation to element itself */
.text-box {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* background-color: #777; */
}

.heading-primary {
  color: #fff;
  text-transform: uppercase;
}

.heading-primary-main {
  display: block;
  font-size: 60px;
  font-weight: 400;
  letter-spacing: 35px;
}

.heading-primary-sub {
  display: block;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: 17.4px;
}


```

## 8. Creating Cool CSS Animations

- CSS animations
- @keyframes: requires start and end position
- animation property: define an animation and use it throughout

To optimize this logo animation (and avoid the logo flux), it would be best to hover the logo-box element in order to trigger the animation on the logo.
.css

```
/* 8. reuse animation on hover*/
.logo-box:hover .logo {
  animation: moveInRight 0.6s ease-in;
}

.heading-primary {
  color: #fff;
  text-transform: uppercase;
  /* 8. fix shaky animations backpart of element gets hidden*/
  backface-visibility: hidden;
}

.heading-primary-main {
  display: block;
  font-size: 60px;
  font-weight: 400;
  letter-spacing: 35px;

  /* 8. */
  animation-name: moveInLeft;
  animation-duration: 1s;
  animation-timing-function: ease-out;
  /*
  alternatives
  animation-delay: 3s;
  animation-iteration-count: 3;
  */
}

.heading-primary-sub {
  display: block;
  font-size: 20px;
  font-weight: 700;
  letter-spacing: 17.4px;

  animation: moveInRight 1s ease-out;
}

/* 8. define the animation*/
@keyframes moveInLeft {
  0% {
    opacity: 0;
    transform: translateX(-100px);
  }

  80% {
    transform: translateX(10px);
  }

  100% {
    opacity: 1;
    transform: translate(0);
  }
}
@keyframes moveInRight {
  0% {
    opacity: 0;
    transform: translateX(100px);
  }

  80% {
    transform: translateX(-10px);
  }

  100% {
    opacity: 1;
    transform: translate(0);
  }
}
```

## 9. Building a Complex Animated Button - Part 1

Discover our tours button animation

pseudo class
btn:link
btn:visited

inline-block elements treated as text: added text-align: center

```
.btn:hover {
  /* move up 3px */
  transform: translateY(-3px);
}
```

set transition to all for 0.2s in the initial state :link, :visited

```

.text-box {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* 9. center button which is treated as text */
  text-align: center;
}

.heading-primary {
  color: #fff;
  text-transform: uppercase;

  /* 8. fix shaky animations backpart of element gets hidden*/
  backface-visibility: hidden;

  /* 9. add whitespace between button and text  */
  margin-bottom: 60px;
}

.btn:link,
.btn:visited {
  text-transform: uppercase;
  text-decoration: none;
  /* first arg padding left & right */
  padding: 15px 40px;
  display: inline-block;
  border-radius: 100px;
  transition: all 0.2s;
}

.btn:hover {
  /* move up 3px */
  transform: translateY(-3px);
  /* x , y , blur, color*/
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

/* when clicked its called :active */
.btn:active {
  transform: translateY(-1px);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.btn-white {
  background-color: #fff;
  color: #777;
}

```

## 10. Building a Complex Animated Button - Part 2

pseudo elements allow us to style certain parts of elements
added new class to index btn-animated

```
.btn::after {
  content: "";
  display: inline-block;
  height: 100%;
  width: 100%;
  border-radius: 100px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  transition: all 0.4s;
}

.btn-white::after {
  background-color: #fff;
}

.btn:hover::after {
  /* increase the size */
  transform: scaleX(1.4) scaleY(1.6);
  /* trick to fade out */
  opacity: 0;
}

.btn-animated {
  /* animation args: name, duration, timing function, delay  */
  animation: moveInBottom 0.5s ease-out 0.75s;
  /* apply styles before animation start */
  animation-fill-mode: backwards;
}
```

# SECTION 3: HOW CSS WORKS: A LOOK BEHIND THE SCENES

## 14.

CSS RULE
Consists of a selector and declaration block

Parsing phase

1. resolve conflicting css declarations
2. process the final css values

Cascade process of combining differenct stylesheets and resolving conflicts between diferent CSS rules and declarations...
Author
User
Brower

Calculate spcificity from left to right, one point for each occurance the left being the most specific.

inline, ids, classes, elements

if all is equal then the winner of the cascade is the last declaration written.

• Each property has an initial value, used if nothing is declared (and if there is no inheritance — see next lecture);
• Browsers specify a root font-size for each page (usually 16px);
• Percentages and relative values are always converted to pixels;
• Percentages are measured relative to their parent’s font-size, if used to specify font-size;
• Percentages are measured relative to their parent’s width, if used to specify lengths;
• em are measured relative to their parent font-size, if used to specify font-size;
• em are measured relative to the current font-size, if used to specify lengths;
• rem are always measured relative to the document’s root font-size;
• vh and vw are simply percentage measurements of the viewport’s height and width.

## 17. How CSS is Parsed, Part 3: Inheritance

• Inheritance passes the values for some specific properties from parents to children — more maintainable code;
• Properties related to text are inherited: font-family, font-size, color, etc;
• The computed value of a property is what gets inherited, not the declared value.
• Inheritance of a property only works if no one declares a value for that property;
• The inherit keyword forces inheritance on a certain property;
• The initial keyword resets a property to its initial value.

## 18. Converting px to rem: An Effective Workflow

Change all absolute pixel units to relative rem units

set the global/root font size to 10.
1 rem is equal to the root font size
1 rem = 10 px

```
html {
  font-size: 10px;
}

// convert to % best practice
// 16px browesr default font size
// 10 / 16 = .625
html {
  font-size: 62.5%;
}
```

Now divide all pixel units by 10 to get the rem unit.

NOTE Respomsive designs good practice is to use rem units

```
*,
*::after *::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}


body {
  font-family: "Lato", sans-serif;
  font-weight: 400;
  line-height: 1.7;
  color: #777;
  padding: 3rem;

  /* 18. */
  box-sizing: border-box;
}
```

## 19. How CSS Renders a Website: The Visual Formatting Model

BOX MODEL

- Content text and images etc.
- Padding: transparet area around the content, inside of the box. Generate whitespace
- Border: goes around the padding and the content
- Margin: whitespace outside the box, space between 2 boxes
- Fill area: area that gets filled with background area and background images, this area excludes the margin

Height & Width
Use box-sizing border-box so that it is easier to work with specified heghts otherwise specified heghts can be altered

BLOCK LEVEL elements, difined by the diplay property

- formatted visually as blocks
- 100% of parents width, create line breaks
- vertically one after another

block level element: display property usually set to block.
for flex-box layout: flex, list item and table also produce block level boxes

INLINE-BOXES

- Content distributed in lines
- Occupies only space content needs
- No line-breaks
- paddings and margins only horizontal (left and right)

INLINE-BLOCK BOXES

- Occupies only contents space
- no line-breaks
- Box-model applies as showed

NORMAL FLOW

- Not floated
- Not absolutely positioned
- Elements laid out according to source order
- Default: position relative

FLOATS

- Element is removed from the normal flow
- Text/inline elements wrap around the floated element
- Container will not adjust its height to the element
- float: left, right

ABSOLUTE POSITIONING

- Elemtn is removed from the normal flow
- No impact on surrounding content or elements
- We use top, bottom, left and right to offset the the element ffrom its reltivelly positioned container
- position: absolute, fixed

## 20. CSS Architecture, Components and BEM

THINK:
Component driven design:

- Think of creating modular building blocks that make up interfaces
- re-usable across the project and even between different projects
- Independant, not dependant on the parent element

BUILD:

- BEM: block elment modifier
  .block{}
  .block**element{}
  .block**element--modifier{}

Block: standalone component that is meaningful on its own
Element: part of a block that has no standalone meaning
Modifier: a differnent version of a block or an element (using flags)

ARCHITECT

- The seven one pattern:

  - 7 different folders for partial Sass files,
  - 1 main Sass file to import all other files into a complied CSS stylesheet

  The 7 Folders:

  1. base/
  2. components/
  3. layout/
  4. pages/
  5. themes/
  6. abstracts/
  7. vendors/ (3rd party CSS)

# SECTIOIN 4 INTRODUCTION TO Sass and NPM

Sass

1. Variables: for resuable values sucha as colors, fonts
2. Nesting: to nest slectors inside of one another
3. Operators: for mathematical operations right inside of CSS
4. Partials & Imports: to write CSS in different files and importing
5. Mixins: reusable pieces of CSS code
6. Functions:
7. Extends: different selectiors inherit declarations that are common to all of them
8. Control directives: for writing complex code using conditionals and loops

## 24. First Steps with Sass: Variables and Nesting

Example of complete code

- use of nesting
- using & creating variables
- grouping components (buttons)

HTML

```
<nav>
  <ul class="navigation">
    <li><a href='#'>About Us</a></li>
    <li><a href='#'>Pricing</a></li>
    <li><a href='#'>Contact Us</a></li>
  </ul>
    <div class="buttons">
      <a class="btn-main " href="#">Sign Up</a>
      <a class="btn-hot" href="#">Get qutote</a>
  </div>
</nav>
```

SCSS

```
* {
margin: 0;
padding: 0;
}

$color-primary: #f9ed69;
$color-secondary: #f08a5d;
$color-tertiary: #b83b5e;
$color-text-dark: #333;
$color-text-light: #eee;

$width-button: 150px;

nav {
  margin: 30px;
  background-color: $color-primary;
  // fix collapsed element caused by using float
  &::after {
    content: "";
    clear: both;
    display: table;
  }
}



.navigation {
  list-style: none;
  float: left;

  li {
    display: inline-block;
    margin-left: 30px;

     &:first-child {
      margin: 0;
    }

    a:link {
      text-decoration: none;
      text-transform: uppercase;
      color: $color-text-dark
    }

  }

}

.buttons {
  float: right;
}

.btn-main:link,
.btn-hot:link {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  text-decoration: none;
  text-transform: uppercase;
  width: $width-button;
  color: $color-text-light;
}

.btn-main {
  &:link {
    background-color: $color-secondary;
  }
  &:hover {
    background-color: darken($color-secondary, 15%);
  }
}

.btn-hot {
  &:link {
    background-color: $color-tertiary;
  }
  &:hover {
    background-color: lighten($color-tertiary, 10%);
  }
}
```

Compiled CSS (compare to Scss)

```
* {
  margin: 0;
  padding: 0;
}

nav {
  margin: 30px;
  background-color: #f9ed69;
}
nav::after {
  content: "";
  clear: both;
  display: table;
}

.navigation {
  list-style: none;
  float: left;
}
.navigation li {
  display: inline-block;
  margin-left: 30px;
}
.navigation li:first-child {
  margin: 0;
}
.navigation li a:link {
  text-decoration: none;
  text-transform: uppercase;
  color: #333;
}

.buttons {
  float: right;
}

.btn-main:link,
.btn-hot:link {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  text-decoration: none;
  text-transform: uppercase;
  width: 150px;
  color: #eee;
}

.btn-main:link {
  background-color: #f08a5d;
}
.btn-main:hover {
  background-color: #ea5717;
}

.btn-hot:link {
  background-color: #b83b5e;
}
.btn-hot:hover {
  background-color: #cb5b7b;
}
```

## 25. First Steps with Sass: Mixins, Extends and Functions

- mixins
- extends
- functions

Changes in the SCSS
SCSS

```
* {
margin: 0;
padding: 0;
}

$color-primary: #f9ed69;
$color-secondary: #f08a5d;
$color-tertiary: #b83b5e;
$color-text-dark: #333;
$color-text-light: #eee;


$width-button: 150px;


@mixin clearfix {
    // fix collapsed element caused by using float
  &::after {
    content: "";
    clear: both;
    display: table;
  }
}

@mixin style-link-text($color) {
  text-decoration: none;
  text-transform: uppercase;
  color: $color;
}

@function divide($a, $b) {
  @return $a / $b;
}

nav {
  margin: divide(60, 2) * 1px;
  background-color: $color-primary;

  @include clearfix;
}



.navigation {
  list-style: none;
  float: left;

  li {
    display: inline-block;
    margin-left: 30px;

     &:first-child {
      margin: 0;
    }

    a:link {
      @include style-link-text($color-text-dark);
    }

  }

}

.buttons {
  float: right;
}

%btn-placeholder {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radius: 100px;
  width: $width-button;
  @include style-link-text($color-text-light);
}

.btn-main {
  &:link {
    @extend %btn-placeholder;
    background-color: $color-secondary;
  }

  &:hover {
    background-color: darken($color-secondary, 15%);
  }
}

.btn-hot {
  &:link {
    @extend %btn-placeholder;
    background-color: $color-tertiary;
  }
  &:hover {
    background-color: lighten($color-tertiary, 10%);
  }
}
```

## 28.

install sass
write script in package.json to watch main.scss file and output to style.css

```
  "scripts": {
    "compile:sass": "sass --watch --update sass/main.scss css/style.css"
  },
```

# Section 5: CONVERTING OUR CSS CODE TO SASS; VARIABLES AND NESTING

## 31. Converting Our CSS Code to Sass: Variables and Nesting

hexadeimal color works in rgba only in Sass
BUG Not compiling as nested, working just does not nest in compiling

## 32. Implementing the 7-1 CSS Architecture with Sass

created partial sass files

- base
- animations
- typography

introduced @use - to import files

refactored the files to 7-1 system

```
C:.
├───dist
│   ├───css
│   │   └───fonts
│   └───img
├───node_modules
│   ├───.bin
│   ├───anymatch
│   ├───binary-extensions
│   ├───braces
│   │   └───lib
│   ├───chokidar
│   │   ├───lib
│   │   └───types
│   ├───fill-range
│   ├───glob-parent
│   ├───immutable
│   │   └───dist
│   ├───is-binary-path
│   ├───is-extglob
│   ├───is-glob
│   ├───is-number
│   ├───normalize-path
│   ├───picomatch
│   │   └───lib
│   ├───readdirp
│   ├───sass
│   │   └───types
│   │       ├───legacy
│   │       ├───logger
│   │       ├───util
│   │       └───value
│   ├───source-map-js
│   │   └───lib
│   └───to-regex-range
└───sass
    ├───abstracts
    ├───base
    ├───components
    ├───layouts
    └───pages
```

## 33. Review: Responsive Design Principles and Layout Types

4 principles

1. fluid layouts:
   1. to allow viewport to adapt to the current viewport width / height
   2. Use % or ( vh / vw ) unit instead of px for elements that should adapt to viewport (usually layout)
   3. use max-width instead of width
2. responsive units
   1. use rem unit istead of px for most lengths
3. flexible images
   1. by degault images dont scale
   2. always use % for image dimensions with max-width property
4. media queries
   1. to change CSS on certain viewpoint widths/breakpoints

3 Layout Types:

1. float layouts
2. flexbox
3. CSS Grid

## 34. Building a Custom Grid with Floats

- calc()
- :not pseudo class
- attribute selector
- build a grid system
- :not
- clearfix

NOTE tip

```
  // starts with col-
  [class^="col-] {

  }
    // contains col-
    [class*="col-] {

  }
    // ends with col-
    [class$="col-] {

  }
```

NOTE basic math used to build a grid system
_grid.scss_

```
.row {
  max-width: $grid-width;
  background-color: #eee;
  margin: 0 auto;

  &:not(:last-child) {
    margin-bottom: $gutter-vertical;
  }

  @include clearfix;

  // attributes that start with col-
  [class^="col-"] {
    background-color: orangered;
    float: left;

    &:not(:last-child) {
      margin-right: $gutter-horizontal;
    }
  }

  .col-1-of-2 {
    width: calc((100% - #{$gutter-horizontal}) / 2);
  }

  .col-1-of-3 {
    width: calc((100% - 2 * #{$gutter-horizontal}) / 3);
  }

  .col-2-of-3 {
    width: calc(
      2 * ((100% - 2 * #{$gutter-horizontal}) / 3) + #{$gutter-horizontal}
    );
  }

  .col-1-of-4 {
    width: calc((100% - 3 * #{$gutter-horizontal}) / 4);
  }

  .col-2-of-4 {
    width: calc(
      2 * ((100% - 3 * #{$gutter-horizontal}) / 4) + #{$gutter-horizontal}
    );
  }

  .col-3-of-4 {
    width: calc(
      3 * ((100% - 3 * #{$gutter-horizontal}) / 4) + 2 * #{$gutter-horizontal}
    );
  }
}
```

## 35. Building the About Section - Part 1

Using grid.
utility class u center text
used skew for heading

NOTE tip; We made the h2 inline block anc created a utility class to center the text

````

    <main>
      <section class="section-about">
        <div class="u-center-text u-margin-bottom-8">
          <h2 class="heading-secondary">
            Exciting tours for adventurous people
          </h2>
        </div>

        <div class="row">
          <div class="col-1-of-2">Text Content</div>
          <div class="col-1-of-2">Image Composition</div>
        </div>
      </section>
    </main>


    ```


_typography.scss
    ```
    .heading-secondary {
  font-size: 3.5rem;
  text-transform: uppercase;
  font-weight: 700;
  display: inline-block;
  background-image: linear-gradient(
    to right,
    $color-primary-light,
    $color-primary-dark
  );
  -webkit-background-clip: text;
  color: transparent;
  letter-spacing: 0.2rem;
  transition: all 0.2s;

  &:hover {
    transform: skewY(2deg) skewX(15deg) scale(1.1);
    text-shadow: 0.5rem 1rem 2rem rgba($color-black, 0.2);
  }
}
````

## 36. Building the About Section - Part 2

about section after the header

typography.scss

```
.heading-tertiary {
  font-size: $default-font-size;
  font-weight: 700;
  text-transform: uppercase;
}

.paragraph {
  font-size: $default-font-size;

  &:not(:last-of-type) {
    margin-bottom: 3rem;
  }
}
```

button.scss

```
.btn-text {
  &:link,
  &:visited {
    font-size: $default-font-size;
    color: $color-primary;
    display: inline-block;
    text-decoration: none;
    border-bottom: 1px solid $color-primary;
    padding: 3px;
    transition: all 0.2s;
  }

  &:hover {
    background-color: $color-primary;
    color: $color-white;
    box-shadow: 0 1rem 2rem rgba($color-black, 0.15);
    transform: translateY(-2px);
  }

  &:active {
    box-shadow: 0 0.5rem 1rem rgba($color-black, 0.15);
    transform: translateY(0);
  }
}
```

## 37. Building the About Section - Part 3

build 3 images, add border and scale on hover
composition.scss

imported to main.scss
index.html

```
          <div class="col-1-of-2">
            <div class="composition">
              <img
                src="img/nat-1.jpg"
                alt=""
                class="composition__photo composition__photo--p1"
              /><img
                src="img/nat-2.jpg"
                alt=""
                class="composition__photo composition__photo--p2"
              /><img
                src="img/nat-3.jpg"
                alt=""
                class="composition__photo composition__photo--p3"
              />
            </div>
          </div>
```

- outline, outline-offset
- left (for margin)
- z-index: for stacking the images
- scale

  define width and left/right of images in percentages if possible
  left definition: Specifies how far an absolutely positioned box's left margin edge is offset to the right of the left edge of the box's 'containing block'.

composition.scss

```
.composition {
  position: relative;

  &__photo {
    width: 55%;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
    // border-radius: 2px;

    // reference for absolute is 1st parent referenced with set position,
    // i.e top left corner of .composition
    position: absolute;
    z-index: 10;
    transition: all 0.2s;

    transition: border-radius 0s;

    outline-offset: 2rem;

    // place images
    &--p1 {
      left: 0;
      top: -2rem;
    }
    &--p2 {
      right: 0;
      top: 2rem;
    }
    &--p3 {
      left: 20%;
      top: 10rem;
    }

    &:hover {
      outline: 1.5rem solid $color-primary;
      transform: scale(1.05) translateY((-0.5rem));
      box-shadow: 0 2.5rem 4rem rgba($color-black, 0.5);
      z-index: 20;
      border-radius: 0;
    }
  }

  // composition:hover composition__photo:(:hover)
  &:hover & __photo:not(:hover) {
    transform: scale(0.95);
  }
}

```

## 38. Building the Features Section

- How to include and use an icon font
- Another way of creating skewed section design
- How and when to use the direct child selector

NOTE dowloaded fonts from : https://github.com/linea-io/Linea-Iconset

TIP: do not scale our grid, our original grid should remain unchanged.

index.html

````
    <section class="section-features">

    <div class="row">
      <div class="col-1-of-4">
        <div class="feature-box">
          <i class="featur-box__icon icon-basic-world"></i>
          <h3 class="heading-tertieary">Explore the world</h3>
          <p class="feature-box__text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit.
          </p>
        </div>
      </div>
    </div>
    ```
````

feature-box.scss

```
.feature-box {
  background-color: rgba($color-white, 0.8);
  font-size: 1.5rem;
  padding: 2.5rem;
  text-align: center;
  border-radius: 3px;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

  // icon
  transition: transform 0.3s;
  &__icon {
    font-size: 6rem;
    margin-bottom: 0.5rem;
    // GRADIANT COLORING
    display: inline-block;
    background-image: linear-gradient(
      to right,
      $color-primary-light,
      $color-primary-dark
    );
    -webkit-background-clip: text;
    color: transparent;
  }

  &:hover {
    transform: translateY(-1.5rem) scale(1.03);
  }
}
```

home.scss

```
.section-features {
  padding: 20rem 0;

  background-image: linear-gradient(
      to right bottom,
      rgba($color-primary-light, 0.8),
      rgba($color-primary-dark, 0.8)
    ),
    url(../img/nat-4.jpg);
  background-size: cover;
  transform: skewY(-7deg);

  // raise section to remvove the white polygon shape left from using skew()
  margin-top: -10rem;

  // direct child of selection features, .section-features > *
  & > * {
    transform: skewY(7deg);
  }
}
```

## 39. Building the Tours Section - Part 1

Most popular tours section:

- Build rotating card
- Use perspective in CSS
- Use the backface-visibility property
- Background blend modes
- When to use box-decoration-break

index.html

```
    <section class="section-tours">
        <div class="u-center-text u-margin-bottom-big">
          <h2 class="heading-secondary">Most popular tours</h2>
        </div>

        <div class="row">
          <div class="col-1-of-3">
            <div class="card">
              <div class="card__side card__side--front">FRONT</div>
              <div class="card__side card__side--back card__side--back-1">
                BACK
              </div>
            </div>
          </div>

          <div class="col-1-of-3">Col 1 of 3</div>
          <div class="col-1-of-3">Col 1 of 3</div>
        </div>
      </section>
```

home.scss

```
.section-tours {
  background-color: $color-grey-light-1;
  padding: 25rem 0 50rem 0;
  margin-top: -10rem;
}

```

perspective
card.scss

```
.card {
  // perspective must be on parent element
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  height: 50rem;

  &__side {
    color: #fff;
    font-size: 2rem;

    height: 50rem;
    transition: all 0.8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    // hide back of element
    backface-visibility: hidden;
    border-radius: 3px;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &--front {
      background-color: $color-white;
    }

    &--back {
      transform: rotateY(180deg);

      &-1 {
        background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        );
      }
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  &:hover &__side--back {
    transform: rotateY(0);
  }
}

```

## 40. Building the Tours Section - Part 2

background-blend-mode: screen;
overflow-hidden: hide the overlap on a parent element caused from an image in our example

adding pictures
card.scss

```
// 39.
.card {
  // FUNCTIONALITY. perspective must be on parent element
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  height: 52rem;

  &__side {
    height: 52rem;
    transition: all 0.8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    // hide back of element
    backface-visibility: hidden;
    border-radius: 3px;
    overflow: hidden;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &--front {
      background-color: $color-white;
    }

    &--back {
      transform: rotateY(180deg);

      &-1 {
        background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        );
      }
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  &:hover &__side--back {
    transform: rotateY(0);
  }

  // 40. FRONT SIDE STYLING
  &__picture {
    background-size: cover;
    height: 23rem;
    background-blend-mode: screen;
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);

    &--1 {
      // path relative to compiled css file
      background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        ),
        url(../img/nat-5.jpg);
    }
    &--2 {
      background-image: url(../img/nat-5.jpg);
    }
    &--3 {
      background-image: url(../img/nat-5.jpg);
    }
  }

  &__heading {
    font-size: 2.8rem;
    font-weight: 300;
    text-transform: uppercase;
    text-align: right;
    color: $color-white;
    position: absolute;
    top: 12rem;
    right: 2rem;
    width: 75%;
  }

  &__heading-span {
    padding: 1rem 1.5rem;
    // treat the two lines as 2 entities
    // so the padding is applied evenly on both lines
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;

    &--1 {
      background-image: linear-gradient(
        to right bottom,
        rgba($color-secondary-light, 0.85) rgba($color-secondary-dark, 0.85)
      );
    }
  }

  &__details {
    padding: 3rem;

    ul {
      list-style: none;
      width: 80%;

      // center block element inside a block element
      // 0 =top/bottom, auto= calculated by browser
      margin: 0 auto;

      li {
        text-align: center;
        font-size: 1.5rem;
        padding: 1rem;

        &:not(:last-child) {
          border-bottom: 1px solid $color-grey-light-2;
        }
      }
    }
  }
}

```

index.html

```
  <section class="section-tours">
        <div class="u-center-text u-margin-bottom-big">
          <h2 class="heading-secondary">Most popular tours</h2>
        </div>

        <div class="row">
          <div class="col-1-of-3">
            <div class="card">
              <div class="card__side card__side--front">
                <div class="card__picture card__picture--1">&nbsb</div>
                <h4 class="card__heading">
                  <span class="card__heading-span card__heading-span--1">
                    The Sea Explorer</span
                  >
                </h4>
                <div class="card__details">
                  <ul>
                    <li>3 day tour</li>
                    <li>Up to 30 people</li>
                    <li>2 tour guides</li>
                    <li>Sleep in cozy hotels</li>
                    <li>Difficulty: easy</li>
                  </ul>
                </div>
              </div>
              <!-- 41. -->
              <div class="card__side card__side--back card__side--back-1">
                <div class="card__cta">
                  <div class="card__price-box">
                    <p class="card__price-only">Only</p>
                    <p class="card__price-value">$297</p>
                  </div>
                  <a href="#" class="btn btn--white">Book now!</a>
                </div>
              </div>
            </div>
          </div>
          <!-- card 2 middle -->
          <div class="col-1-of-3">
            <div class="card">
              <div class="card__side card__side--front">
                <div class="card__picture card__picture--2">&nbsb</div>
                <h4 class="card__heading">
                  <span class="card__heading-span card__heading-span--2">
                    The forest hiker</span
                  >
                </h4>
                <div class="card__details">
                  <ul>
                    <li>7 day tour</li>
                    <li>Up to 40 people</li>
                    <li>6 tour guides</li>
                    <li>Sleep in provided tents</li>
                    <li>Difficulty: medium</li>
                  </ul>
                </div>
              </div>
              <!-- 41. -->
              <div class="card__side card__side--back card__side--back-2">
                <div class="card__cta">
                  <div class="card__price-box">
                    <p class="card__price-only">Only</p>
                    <p class="card__price-value">$497</p>
                  </div>
                  <a href="#" class="btn btn--white">Book now!</a>
                </div>
              </div>
            </div>
          </div>

          <!-- card 3 end (left to right) -->
          <div class="col-1-of-3">
            <div class="card">
              <div class="card__side card__side--front">
                <div class="card__picture card__picture--3">&nbsb</div>
                <h4 class="card__heading">
                  <span class="card__heading-span card__heading-span--3">
                    The Snow Adventurer</span
                  >
                </h4>
                <div class="card__details">
                  <ul>
                    <li>5 day tour</li>
                    <li>Up to 15 people</li>
                    <li>3 tour guides</li>
                    <li>Sleep in provided tents</li>
                    <li>Difficulty: hard</li>
                  </ul>
                </div>
              </div>
              <!-- 41. -->
              <div class="card__side card__side--back card__side--back-3">
                <div class="card__cta">
                  <div class="card__price-box">
                    <p class="card__price-only">Only</p>
                    <p class="card__price-value">$297</p>
                  </div>
                  <a href="#" class="btn btn--white">Book now!</a>
                </div>
              </div>
            </div>
          </div>
        </div>
```

## 41. Building the Tours Section - Part 3

Back of tour cards:

index.html code updated for this section in the section 40 of notes.

button.scss

```
 &--green {
    background-color: $color-primary;
    color: $color-white;

    &::after {
      background-color: $color-primary;
    }
  }
```

padding changed
home.scss

```
.section-tours {
  background-color: $color-grey-light-1;
  padding: 25rem 0 15rem 0;
  margin-top: -10rem;
}
```

styling cards in tour section.
cards.scss

```
.card {
  // FUNCTIONALITY. perspective must be on parent element
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  height: 52rem;

  &__side {
    height: 52rem;
    transition: all 0.8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    // hide back of element
    backface-visibility: hidden;
    border-radius: 3px;
    overflow: hidden;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &--front {
      background-color: $color-white;
    }

    &--back {
      transform: rotateY(180deg);

      &-1 {
        background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        );
      }
      // 41.
      &-2 {
        background-image: linear-gradient(
          to right bottom,
          $color-primary-light,
          $color-primary-dark
        );
      }
      &-3 {
        background-image: linear-gradient(
          to right bottom,
          $color-tertiary-light,
          $color-tertiary-dark
        );
      }
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  &:hover &__side--back {
    transform: rotateY(0);
  }

  // 40. FRONT SIDE STYLING
  &__picture {
    background-size: cover;
    height: 23rem;
    background-blend-mode: screen;
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    // clip path breaks overflow so we add it manually below
    clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    border-top-right-radius: 3px;
    border-top-left-radius: 3px;

    &--1 {
      // path relative to compiled css file
      background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        ),
        url(../img/nat-5.jpg);
    }
    &--2 {
      background-image: linear-gradient(
          to right bottom,
          $color-primary-light,
          $color-primary-dark
        ),
        url(../img/nat-6.jpg);
    }
    &--3 {
      background-image: linear-gradient(
          to right bottom,
          $color-tertiary-light,
          $color-tertiary-dark
        ),
        url(../img/nat-7.jpg);
    }
  }

  &__heading {
    font-size: 2.8rem;
    font-weight: 300;
    text-transform: uppercase;
    text-align: right;
    color: $color-white;
    position: absolute;
    top: 12rem;
    right: 2rem;
    width: 75%;
  }

  &__heading-span {
    padding: 1rem 1.5rem;
    // treat the two lines as 2 entities
    // so the padding is applied evenly on both lines
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;

    &--1 {
      background-image: linear-gradient(
        to right bottom,
        rgba($color-secondary-light, 0.85) rgba($color-secondary-dark, 0.85)
      );
    }
  }

  &__details {
    padding: 3rem;

    ul {
      list-style: none;
      width: 80%;

      // center block element inside a block element
      // 0 =top/bottom, auto= calculated by browser
      margin: 0 auto;

      li {
        text-align: center;
        font-size: 1.5rem;
        padding: 1rem;

        &:not(:last-child) {
          border-bottom: 1px solid $color-grey-light-2;
        }
      }
    }
  }

  // 41. BACK OF CARD STYLING
  &__cta {
    // centering
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    // width fixes the alignment of text in the button
    // because the price box width is adapting to width of the cta box
    width: 90%;
    text-align: center;
  }

  &__price-box {
    text-align: center;
    margin-bottom: 8rem;
    color: $color-white;
  }

  &__price-only {
    font-size: 1.4rem;
    text-transform: uppercase;
  }

  &__price-value {
    font-size: 6rem;
    font-weight: 100;
  }
}
```

## 42. Building the Stories Section - Part 1

- How to make text flow around shapes with shape-outside and float
- How to apply filter to images
- Create background video covering an entire section
- Use the <video> HTML element
- Object-fit property, when and how to use

index.html

```
    <section class="section-stories">
        <div class="u-center-text u-margin-bottom-big">
          <h2 class="heading-secondary">We make people genuinely happy</h2>
        </div>
        <!-- stroy component -->
        <div class="row">
          <div class="story">
            <figure class="story__shape">
              <img
                src="img/nat-8.jpg"
                alt="Person on a tour"
                class="story__img"
              />
            </figure>
            <div class="story__text">
              <h3 class="heading-tertiary u-margin-bottom-small">
                I had the best week ever with my family
              </h3>
              <p>
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Veniam
                assumenda similique dignissimos. Lorem ipsum dolor sit, amet
                consectetur adipisicing elit. Veniam assumenda similique
                dignissimos. Lorem ipsum dolor sit, amet consectetur adipisicing
                elit. Veniam assumenda similique dignissimos.
              </p>
            </div>
          </div>
        </div>
      </section>
```

home.scss

```
.section-stories {
  // padding top/bottom, left/right
  padding: 15rem 0;
  background-color: $color-grey-light-1;
}
```

story.scss

```
.story {
  width: 75%;
  margin: 0 auto;
  box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
  background-color: $color-white;
  border-radius: 3px;
  padding: 6rem;
  padding-left: 9rem;
  font-size: $default-font-size;
  transform: skewX(-12deg);

  &__shape {
    content: " ";
    // square
    width: 15rem;
    height: 15rem;

    float: left;
    // define vectorised shape,
    // element must be floated and have defiened dimensions
    // for shape-outside to work
    // 1st arg radius
    -webkit-shape-outside: circle(50% at 50% 50%);
    shape-outside: circle(50% at 50% 50%);

    // turn square to circle
    -webkit-clip-path: circle(50% at 50% 50%);
    clip-path: circle(50% at 50% 50%);

    // at time of recording
    // multiple transform on one element is not possible
    // NOTE use transform to move around elements that are floated (better than margin)
    transform: translateX(-3rem) skewX(12deg);
  }

  // height is 100% of the &__shape width
  &__img {
    height: 100%;
  }
  &__text {
    transform: skewX(12deg);
  }
}
```

## 43. Building the Stories Section - Part 2

story.scss (added this line top-level)
`  background-color: rgba($color-white, 60%);`

story section
index.html

```
        <div class="row">
          <div class="story">
            <figure class="story__shape">
              <img
                src="img/nat-8.jpg"
                alt="Person on a tour"
                class="story__img"
              />
              <!-- 43. -->
              <figcaption class="story__caption">Mary Smith</figcaption>
            </figure>
            <div class="story__text">
              <h3 class="heading-tertiary u-margin-bottom-small">
                I had the best week ever with my family
              </h3>
              <p>
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Veniam
                assumenda similique dignissimos. Lorem ipsum dolor sit, amet
                consectetur adipisicing elit. Veniam assumenda similique
                dignissimos. Lorem ipsum dolor sit, amet consectetur adipisicing
                elit. Veniam assumenda similique dignissimos.
              </p>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="story">
            <figure class="story__shape">
              <img
                src="img/nat-9.jpg"
                alt="Person on a tour"
                class="story__img"
              />
              <!-- 42. -->
              <figcaption class="story__caption">Jack Wilson</figcaption>
            </figure>
            <div class="story__text">
              <h3 class="heading-tertiary u-margin-bottom-small">
                WOW! My life is completely different now
              </h3>
              <p>
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Veniam
                assumenda similique dignissimos. Lorem ipsum dolor sit, amet
                consectetur adipisicing elit. Veniam assumenda similique
                dignissimos. Lorem ipsum dolor sit, amet consectetur adipisicing
                elit. Veniam assumenda similique dignissimos.
              </p>
            </div>
          </div>
        </div>
      </section>
      <!-- button -->
      <div class="u-center-text u-margin-top-huge">
        <a href="#" class="btn-text">Read all stories &rarr;</a>
      </div>

```

home.scss

```
.section-stories {
  // padding top/bottom, left/right
  padding: 15rem 0;
  background-color: $color-grey-light-1;
}
```

story.scss

```
.story {
  width: 75%;
  margin: 0 auto;
  box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
  background-color: $color-white;
  border-radius: 3px;
  padding: 6rem;
  padding-left: 9rem;
  font-size: $default-font-size;
  transform: skewX(-12deg);

  &__shape {
    content: " ";
    // square
    width: 15rem;
    height: 15rem;

    float: left;
    // define vectorised shape,
    // element must be floated and have defiened dimensions
    // for shape-outside to work
    // 1st arg radius
    -webkit-shape-outside: circle(50% at 50% 50%);
    shape-outside: circle(50% at 50% 50%);

    // turn square to circle
    -webkit-clip-path: circle(50% at 50% 50%);
    clip-path: circle(50% at 50% 50%);

    // at time of recording
    // multiple transform on one element is not possible
    // NOTE use transform to move around elements that are floated (better than margin)
    transform: translateX(-3rem) skewX(12deg);
    // 42. make relative for the &__caption position absolute to work
    position: relative;
  }

  // height is 100% of the &__shape width
  &__img {
    // this transition fixed the bug on hover
    // transition did not work after hover state
    transition: transform 0.5s;
    height: 100%;
    transform: translateX(-4rem) scale(1.4);
    backface-visibility: hidden;
  }

  &__text {
    transform: skewX(12deg);
  }

  // position caption dead center
  &__caption {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, 20%);
    color: $color-white;
    text-transform: uppercase;
    font-size: 1.7rem;
    text-align: center;
    opacity: 0;
    transition: all 0.5s;
    // fix shaky glitch
    backface-visibility: hidden;
  }

  &:hover &__caption {
    opacity: 1;
    transform: translate(-50%, -50%);
  }

  &:hover &__img {
    transform: translateX(-4rem) scale(1);
    // filters, blur and reduce brightness (make img darker)
    filter: blur(3px) brightness(80%);
    transition: all 0.5s;
  }
}

```

## 44. Building the Stories Section - Part 3

Get free videos for coverpages at coverr

Video portion only
index.html

```
        <div class="bg-video">
          <video class="bg-video__content" autoplay muted loop>
            <source src="img/video.mp4" type="video/mp4" <source
            src="img/video.webm" type="video/webm"
          </video>
          Your browser is not supported!
        </div>
```

bg-video.scss

```
.bg-video {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: -1;
  opacity: 0.15;
  overflow: hidden;

  &__content {
    height: 100%;
    width: 100%;
    // fit image to section and respecting the video aspec-ratio
    object-fit: cover;
  }
}
```

modification, position relative
home.scss

```
.section-stories {
  // padding top/bottom, left/right
  padding: 15rem 0;
  position: relative;
}

```

story.scss

```
.story {
  width: 75%;
  margin: 0 auto;
  box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
  background-color: rgba($color-white, 60%);
  border-radius: 3px;
  padding: 6rem;
  padding-left: 9rem;
  font-size: $default-font-size;
  transform: skewX(-12deg);

  &__shape {
    content: " ";
    // square
    width: 15rem;
    height: 15rem;

    float: left;
    // define vectorised shape,
    // element must be floated and have defiened dimensions
    // for shape-outside to work
    // 1st arg radius
    -webkit-shape-outside: circle(50% at 50% 50%);
    shape-outside: circle(50% at 50% 50%);

    // turn square to circle
    -webkit-clip-path: circle(50% at 50% 50%);
    clip-path: circle(50% at 50% 50%);

    // at time of recording
    // multiple transform on one element is not possible
    // NOTE use transform to move around elements that are floated (better than margin)
    transform: translateX(-3rem) skewX(12deg);
    // 42. make relative for the &__caption position absolute to work
    position: relative;
  }

  // height is 100% of the &__shape width
  &__img {
    // this transition fixed the bug on hover
    // transition did not work after hover state
    transition: transform 0.5s;
    height: 100%;
    transform: translateX(-4rem) scale(1.4);
    backface-visibility: hidden;
  }

  &__text {
    transform: skewX(12deg);
  }

  // position caption dead center
  &__caption {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, 20%);
    color: $color-white;
    text-transform: uppercase;
    font-size: 1.7rem;
    text-align: center;
    opacity: 0;
    transition: all 0.5s;
    // fix shaky glitch
    backface-visibility: hidden;
  }

  &:hover &__caption {
    opacity: 1;
    transform: translate(-50%, -50%);
  }

  &:hover &__img {
    transform: translateX(-4rem) scale(1);
    // filters, blur and reduce brightness (make img darker)
    filter: blur(3px) brightness(80%);
    transition: all 0.5s;
  }
}
```

## 45. Building the Booking Section - Part 1

- solid-color gradients
- Heneral and adjacent sibling selectors
- the ::input-placeholder pseudo-element
- use :focus, :invalid, placeholder-shown and :checked pseudo classes
- custom radio buttons

index.html

```
<section class="section-book">
        <div class="row">
          <div class="book">
            <div class="book__form">
              <form action="#" class="form">
                <div class="u-margin-bottom-medium">
                  <h2 class="heading-secondary">Start booking now</h2>
                </div>

                <div class="form__group">
                  <input
                    type="text"
                    class="form__input"
                    placeholder="Full name"
                    id="name"
                    required
                  />
                  <label for="name" class="form__label">Full name</label>
                </div>

                <div class="form__group">
                  <input
                    type="email"
                    class="form__input"
                    placeholder="Email address"
                    id="email"
                    required
                    autocomplete="off"
                  />
                  <label for="email" class="form__label">Email address</label>
                </div>
              </form>
            </div>
          </div>
        </div>
      </section>
```

home.scss

```

      .book {

background-image: linear-gradient(
105deg,
rgba($color-white, 0.9),
      rgba($color-white, 0.9) 50%,
transparent 50%
),
url(../../dist/img/nat-10.jpg);
background-size: 100%;
border-radius: 3px;
box-shadow: 0 1.5rem 4rem rgba($color-black, 0.2);
height: 50rem;

&\_\_form {
width: 50%;
padding: 6rem;
}
}

```

## 46. Building the Booking Section - Part 2

HTML in previous section is valid for this section.

When hiding elements note the opacity 0 and visibility hidden are both used.
Hide

use :focus, :invalid, placeholder-shown and :checked pseudo classes
form.scss

```
.form {
  &__group:not(:last-child) {
    margin-bottom: 2rem;
  }

  &__input {
    font-size: 1.5rem;
    // inputs dont inherit font properties by default
    font-family: inherit;
    color: inherit;
    padding: 1.5rem 2rem;
    border-radius: 2px;
    background-color: rgba($color-white, 0.5);
    border: none;
    border-bottom: 3px solid transparent;
    width: 90%;
    display: block;

    &:focus {
      outline: none;
      // make element visible to users without a mouse
      box-shadow: 0 1rem 2rem rgba($color-black, 0.1);
      border-bottom: 3px solid $color-primary;
    }

    // when invalid implement this style
    &:focus:invalid {
      border-bottom: 3px solid $color-secondary-dark;
    }

    &::-webkit-input-placeholder {
      color: $color-grey-dark-2;
    }
  }
  &__label {
    font-size: 1.2rem;
    font-weight: 700;
    // display block to use following box properties
    margin-left: 2rem;
    margin-top: 0.7rem;
    display: block;
    transition: all 0.3s;
  }

  // Sibling selector. show text on input
  &__input:placeholder-shown + &__label {
    // possible to animate opacity not visibility
    opacity: 0;
    visibility: hidden;
     transform: translateY(-4rem);
  }
}
```

## 47. Building the Booking Section - Part 3

HTML:

- connect a groups by giving each input the same name
- connect label and id of same group with id and for attributes

- trick to style radio buttons
- updated utilities class to have !important property

index.html

```
  <div class="form__group u-margin-bottom-medium">
                  <div class="form__radio-group">
                    <input
                      type="radio"
                      class="form__radio-input"
                      id="small"
                      name="size"
                    />
                    <label for="small" class="form__radio-label">
                      <span class="form__radio-button"></span>
                      Small tour group
                    </label>
                  </div>

                  <div class="form__radio-group">
                    <input
                      type="radio"
                      class="form__radio-input"
                      id="large"
                      name="size"
                    />
                    <label for="large" class="form__radio-label">
                      <span class="form__radio-button"></span>
                      Large tour group
                    </label>
                  </div>
                </div>

                <div class="form__group">
                  <button class="btn btn--green">Next step &rarr;</button>
                </div>
```

form.scss

```
  &__radio-group {
    width: 49%;
    display: inline-block;
  }

  // hide radio button
  &__radio-input {
    display: none;
  }

  &__radio-label {
    font-size: $default-font-size;
    cursor: pointer;

    padding-left: 4.5rem;
    position: relative;
  }

  &__radio-button {
    height: 3rem;
    width: 3rem;
    border: 5px solid $color-primary;
    border-radius: 50%;
    display: inline-block;
    position: absolute;
    left: 0;
    top: -0.4rem;

    // inner element circle
    // content and display property must be specified in pseudo elements
    &::after {
      content: "";
      display: block;
      height: 1.3rem;
      width: 1.3rem;
      border-radius: 50%;
      // position circle
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: $color-primary;

      // hide inner circle
      opacity: 0;
      transition: opacicty 0.2s;
    }
  }

  &__radio-input:checked ~ &__radio-label &__radio-button::after {
    opacity: 1;
  }
```

Snippet of what is important for this section.
button.scss

```
.btn {
  &,
  /* 9. Building a Complex Animated Button, discover our tour button */
  &:link,
  &:visited {
    text-transform: uppercase;
    text-decoration: none;
    /* first arg padding left & right */
    padding: 1.5rem 4rem;
    display: inline-block;
    border-radius: 10rem;
    transition: all 0.2s;
    /* 10. */
    position: relative;
    font-size: $default-font-size;

    // 47. change for the <button> element (book tour)
    border: none;
    cursor: pointer;
  }

  &:active,
  &:focus {
    transform: translateY(-1px);
    box-shadow: 0 0.5rem 1rem rgba($color-black, 0.2);
  }
```

## 48. Building the Footer

index.html

```
   <footer class="footer">
      <div class="footer__logo-box">
        <img src="img/logo-green-2x.png" alt="Full logo" class="footer" />
      </div>
      <div class="row">
        <div class="col-1-of-2">
          <div class="footer__navigation">
            <ul class="footer__list">
              <li class="footer__item">
                <a href="#" class="footer__link">Company</a>
              </li>
              <li class="footer__item">
                <a href="#" class="footer__link">Contact us</a>
              </li>
              <li class="footer__item">
                <a href="#" class="footer__link">Careers</a>
              </li>
              <li class="footer__item">
                <a href="#" class="footer__link">Privacy policy</a>
              </li>
              <li class="footer__item">
                <a href="#" class="footer__link">Terms</a>
              </li>
            </ul>
          </div>
        </div>
        <div class="col-1-of-2">
          <p class="footer__copyright">
            Built by <a href="#" class="footer__link">YK</a> from an online
            course. <a href="A" class="footer__link">Advanced CSS and Sass</a>.
            Copyright &copy; by Yanal Kamal.
          </p>
        </div>
      </div>
    </footer>
```

footer.scss

```
.footer {
  background-color: $color-grey-dark-3;
  padding: 10rem 0;
  font-size: 1.4rem;
  color: $color-grey-light-1;

  &__logo-box {
    // image is inline element (behaves like text)
    text-align: center;
    margin-bottom: 8rem;
  }

  &__logo {
    width: 15rem;
    height: auto;
  }

  &__navigation {
    border-top: 1px solid $color-grey-dark-2;
    padding-top: 2rem;
    // shorten the border top length with:
    display: inline-block;
  }

  &__list {
    list-style: none;
  }

  &__item {
    display: inline-block;

    &:not(:last-child) {
      margin-right: 1.5rem;
    }
  }

  &__link {
    &:link,
    &:visited {
      color: $color-grey-light-1;
      background-color: $color-grey-dark-3;
      text-decoration: none;
      text-transform: uppercase;
      display: inline-block;
      transition: all 0.2s;
    }

    &:hover,
    &:active {
      color: $color-primary;
      box-shadow: 0 1rem 2rem rgba($color-black, 0.4);
      transform: rotate(5deg) scale(1.3);
    }
  }

  &__copyright {
    border-top: 1px solid $color-grey-dark-2;
    padding-top: 2rem;
    width: 80%;
    float: right;
  }
}

```

## 49. Building the Navigation - Part 1

- How the checkox hack works
- Custom animation timing functions using bezier curves
- How to animate solid-color gradients
- How to use transform-origin

1. check-box that will be hidden
2. add label that is connected to the checkbox (nav button)
3. reveal navigation when checked

-radial-gradient()
index.html

```
    <div class="navigation">
      <input type="checkbox" class="navigation__checkbox" id="navi-toggle" />

      <label for="navi-toggle" class="navigation__button">MENU</label>

      <div class="navigation__background">&nbsp;</div>

      <nav class="navigation__nav">
        <ul class="navigation__list">
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>01</span> About Natours</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>02</span> Your benefits</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>03</span> Popular tours</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"><span>04</span> Stories</a>
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"><span>05</span> Book now</a>
          </li>
        </ul>
      </nav>
    </div>
```

footer.scss

```
.navigation {
  &__checkbox {
    display: none;
  }

  &__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    position: fixed;
    top: 6rem;
    right: 6rem;
    border-radius: 50%;
    z-index: 2000;
  }

  &__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;

    transform: scale(80);
  }

  &__nav {
    height: 100vh;
    width: 100%;
    position: fixed;
    top: 0;
    top: 0;
    z-index: 1500;
  }

  // center nav items to middle of page
  &__list {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate((-50%, -50%));
    list-style: none;
    text-align: center;
  }

  &__item {
    margin: 1rem;
  }

  &__link {
    &:link,
    &:visited {
      display: inline-block;
      font-size: 3rem;
      font-weight: 300;
      padding: 1rem 2rem;
      color: $color-white;
      text-decoration: none;
      text-transform: uppercase;
      background-image: linear-gradient(
        120deg,
        // orangered 0%,
        // orangered 50%,
        transparent 0,
        transparent 50%,
        $color-white 50%
      );
      background-size: 220%;
      transition: all 0.4s;

      span {
        margin-right: 1.5rem;
        display: inline-block;
      }
    }

    &:hover,
    &:active {
      background-position: 100%;
      color: $color-primary;
      transform: translateX(1rem);
    }
  }
}
```

## 50. Building the Navigation - Part 2

NOTE easings.net & cubic-bezier.com for referenceing the numbers needed for custom easing timing functions

- How to animate solid-color gradients
  adding removing background once nav checked...

navigation.scss

```
.navigation {
  &__checkbox {
    display: none;
  }

  &__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    position: fixed;
    top: 6rem;
    right: 6rem;
    border-radius: 50%;
    z-index: 2000;
    box-shadow: 0 1rem 3rem rgba($color-black, 0.1);
  }

  &__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;
    // 50. bezier
    transition: transform 0.8s cubic-bezier(0.86, 0, 0.07, 1);
    // transform: scale(80);
  }

  &__nav {
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1500;

    // 50. removing nav items
    opacity: 0;
    width: 0;
    transition: all 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  }

  // center nav items to middle of page
  &__list {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate((-50%, -50%));
    list-style: none;
    text-align: center;
    // 50.
    width: 100%;
  }

  &__item {
    margin: 1rem;
  }

  &__link {
    &:link,
    &:visited {
      display: inline-block;
      font-size: 3rem;
      font-weight: 300;
      padding: 1rem 2rem;
      color: $color-white;
      text-decoration: none;
      text-transform: uppercase;
      background-image: linear-gradient(
        120deg,
        // orangered 0%,
        // orangered 50%,
        transparent 0,
        transparent 50%,
        $color-white 50%
      );
      background-size: 220%;
      transition: all 0.4s;

      span {
        margin-right: 1.5rem;
        display: inline-block;
      }
    }

    &:hover,
    &:active {
      background-position: 100%;
      color: $color-primary;
      transform: translateX(1rem);
    }
  }

  // 50. checkbox hack
  &__checkbox:checked ~ &__background {
    transform: scale(120);
  }

  &__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100%;
  }
}

```

## 51. Building the Navigation - Part 3

Coding up the button

index.html

```
      <nav class="navigation__nav">
        <ul class="navigation__list">
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>01</span> About Natours</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>02</span> Your benefits</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"
              ><span>03</span> Popular tours</a
            >
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"><span>04</span> Stories</a>
          </li>
          <li class="navigation__item">
            <a href="#" class="navigation__link"><span>05</span> Book now</a>
          </li>
        </ul>
      </nav>
    </div>
```

navigations.scss

```
.navigation {
  &__checkbox {
    display: none;
  }

  &__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    position: fixed;
    top: 6rem;
    right: 6rem;
    border-radius: 50%;
    z-index: 2000;
    box-shadow: 0 1rem 3rem rgba($color-black, 0.1);
    // 51. center the nav button lines
    text-align: center;
    cursor: pointer;
  }

  &__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;
    // 50. bezier (whip like transition movement)
    transition: transform 0.8s cubic-bezier(0.86, 0, 0.07, 1);
    // transform: scale(80);
  }

  &__nav {
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1500;

    // 50. removing nav items
    opacity: 0;
    width: 0;
    transition: all 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  }

  // center nav items to middle of page
  &__list {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate((-50%, -50%));
    list-style: none;
    text-align: center;
    // 50.
    width: 100%;
  }

  &__item {
    margin: 1rem;
  }

  &__link {
    &:link,
    &:visited {
      display: inline-block;
      font-size: 3rem;
      font-weight: 300;
      padding: 1rem 2rem;
      color: $color-white;
      text-decoration: none;
      text-transform: uppercase;
      background-image: linear-gradient(
        120deg,
        // orangered 0%,
        // orangered 50%,
        transparent 0,
        transparent 50%,
        $color-white 50%
      );
      background-size: 220%;
      transition: all 0.4s;

      span {
        margin-right: 1.5rem;
        display: inline-block;
      }
    }

    &:hover,
    &:active {
      background-position: 100%;
      color: $color-primary;
      transform: translateX(1rem);
    }
  }

  // 50. FUNCTIONALITY. checkbox hack
  &__checkbox:checked ~ &__background {
    transform: scale(120);
  }

  &__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100%;
  }

  // 51. ICON
  &__icon {
    &::before,
    position: relative;
    margin-top: 3.5rem;
    &,
      width: 3rem;
    &::after {
      height: 2px;
      background-color: $color-grey-dark-3;
      display: inline-block;
    }
    // define content for pseudo element to work
    &::before,
    &::after {
      content: "";
      position: absolute;
      left: 0;
      transition: all 0.2s;
    }

    &::before {
      top: -0.9rem;
    }
    &::after {
      top: 0.9rem;
    }
  }

  &__button:hover &__icon::before {
    top: -1rem;
  }
  &__button:hover &__icon::after {
    top: 1rem;
  }

  // + equals adjacent sibling
  &__checkbox:checked + &__button &__icon {
    background-color: transparent;
  }
  &__checkbox:checked + &__button &__icon::before {
    top: 0;
    transform: rotate(135deg);
  }
  &__checkbox:checked + &__button &__icon::after {
    top: 0;
    transform: rotate(-135deg);
  }

}
```

## 52. Building a Pure CSS Popup - Part 1

- Build a popup with only CSS
- Use the :target pseudo-class
- Create boxes with equal height using display: table-cell
- Create CSS text columns
- Automatically hyphenate words using hyphens

index.html

```
    <div class="popup">
      <div class="popup__content">
        <div class="popup__left">
          <img src="img/nat-8.jpg" alt="Tour photo" class="popup__img" />
          <img src="img/nat-9.jpg" alt="Tour photo" class="popup__img" />
        </div>

        <div class="popup__right">
          <h2 class="heading-secondary u-margin-bottom-small">
            Start booking now
          </h2>
          <h3 class="heading-tertiary u-margin-bottom-small">
            Important &ndash; Please read these terms before booking
          </h3>
          <p class="popup__text">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit.
            Consequuntur quam perferendis hic ut incidunt asperiores nulla quod,
            impedit velit recusandae eius natus officia quaerat nobis aut enim
            beatae voluptatum sed. Velit aspernatur error temporibus quaerat
            totam dolore libero magni pariatur amet voluptates voluptas commodi
            dolorum soluta nisi ipsam quasi at recusandae odit accusantium,
            cumque harum quia aperiam! Nesciunt, deleniti iusto.
          </p>
          <a href="#" class="btn btn--green">Book now</a>
        </div>
      </div>
    </div>
```

popup.scss

```
.popup {
  // backgorund
  height: 100vh;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba($color-black, 0.8);
  z-index: 9999;

  // popup content box
  &__content {
    @include absCenter;

    width: 75%;

    background-color: $color-white;
    box-shadow: 0 2rem 4rem rgba($color-black, 0.2);
    border-radius: 3px;
    display: table;
    overflow: hidden;
  }

  &__left {
    width: 33.3333333333%;
    display: table-cell;
  }

  &__right {
    width: 66.6666666667%;
    display: table-cell;
    vertical-align: middle;
    padding: 3rem 5rem;
  }

  &__img {
    display: block;
    width: 100%;
  }

  &__text {
    font-size: 1.4rem;
    margin-bottom: 4rem;

    // the text columns
    column-count: 2;
    column-gap: 4rem;
    column-rule: 1px solid $color-grey-light-2;

    hyphens: auto;
  }
}
```

## 53. Building a Pure CSS Popup - Part 2

:target

index.html

```
<div class="popup" id="popup">
      <div class="popup__content">
        <div class="popup__left">
          <img src="img/nat-8.jpg" alt="Tour photo" class="popup__img" />
          <img src="img/nat-9.jpg" alt="Tour photo" class="popup__img" />
        </div>

        <div class="popup__right">
          <!-- 53. -->
          <a href="#section-tours" class="popup__close">&times;</a>
          <h2 class="heading-secondary u-margin-bottom-small">
            Start booking now
          </h2>
          <h3 class="heading-tertiary u-margin-bottom-small">
            Important &ndash; Please read these terms before booking
          </h3>
          <p class="popup__text">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit.
            Consequuntur quam perferendis hic ut incidunt asperiores nulla quod,
            impedit velit recusandae eius natus officia quaerat nobis aut enim
            beatae voluptatum sed. Velit aspernatur error temporibus quaerat
            totam dolore libero magni pariatur amet voluptates voluptas commodi
            dolorum soluta nisi ipsam quasi at recusandae odit accusantium,
            cumque harum quia aperiam! Nesciunt, deleniti iusto.
          </p>
          <a href="#" class="btn btn--green">Book now</a>
        </div>
      </div>
    </div>
```

popup.scss

```
.popup {
  // backgorund
  height: 100vh;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba($color-black, 0.8);
  z-index: 9999;
  // 53. add/remove popup
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s;
  &:target {
    opacity: 1;
    visibility: visible;
  }

  // popup content box
  &__content {
    @include absCenter;

    width: 75%;

    background-color: $color-white;
    box-shadow: 0 2rem 4rem rgba($color-black, 0.2);
    border-radius: 3px;
    display: table;
    overflow: hidden;
    opacity: 0;
    // 53. scaled down popup for animation effect
    transform: translate(-50%, -50%) scale(0.25);
    transition: all 0.5s 0.2s;
  }

  &__left {
    width: 33.3333333333%;
    display: table-cell;
  }

  &__right {
    width: 66.6666666667%;
    display: table-cell;
    vertical-align: middle;
    padding: 3rem 5rem;
  }

  &__img {
    display: block;
    width: 100%;
  }

  &__text {
    font-size: 1.4rem;
    margin-bottom: 4rem;

    // the text columns
    -moz-column-count: 2;
    -moz-column-gap: 4rem;
    -moz-column-rule: 1px solid $color-grey-light-2;

    column-count: 2;
    column-gap: 4rem;
    column-rule: 1px solid $color-grey-light-2;

    -moz-hyphens: auto;
    -ms-hyphens: auto;
    -webkit-hyphens: auto;
    hyphens: auto;
  }

  // 53. OPEN STATES
  &:target &__content {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }

  &__close {
    &:link,
    &:visited {
      color: $color-grey-dark;
      position: absolute;
      top: 2.5rem;
      right: 2.5rem;
      font-size: 3rem;
      text-decoration: none;
      display: inline-block;
      transition: all 0.2s;
      line-height: 1;
    }

    &:hover {
      color: $color-primary;
    }
  }
}

```

# Section 6: Natours Project - Advanced Responsive Design

## 55. Mobile-First vs Desktop-First and Breakpoints

Media queries always at the end of the script
Max width desktop first

Min-width mobile first

Breakpoints Best Practice:
Design breaks is best. Add breakpoints by testing going from mobile to desktop. As soon as the visual is weird add a breakpoint

www.Statcounter.com to get data on screen sizes.
The good way is by getting all the most used device screen resolutions and figuring out the optimal breakpoints from there.

## 56. Let's Use the Power of Sass Mixins to Write Media Queries

- How to use Sass mixing to weite all our media queries
- Hot to use the @content and @if Sass directives
- Taking advantage of Chrome DevTools for responsive design

- respond()
- @if
- @media
- @content

NOTE rems/ems in media queries are not affeced by the root font-size. ems are best options for media queries

mixins.scss

```
@mixin clearfix {
  &::after {
    content: "";
    display: table;
    clear: both;
  }
}

// 52. CENTER COMPONENT
@mixin absCenter {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

// 56. MEDIA QUERY MANAGER
/*
0-600px       Phone
600-900px     Tablet-portrait
900-1200px    Tablet-landscape
1200-1800px   is where normal styles are applied
1800px +      Big Desktop

- 56. $breakpoint argument choices (added to base.scss)
- phone
- tab-port
- tab-land
- big-desktop
DIVIDE REM BY 16 TO GET THE EM VALUE
*/
@mixin respond($breakpoint) {
  // 600px / 16
  @if $breakpoint == phone {
    @media (max-width: 37.5em) {
      @content;
    }
  }

  //900px / 16
  @if $breakpoint == tab-port {
    @media (max-width: 56.25em) {
      @content;
    }
  }

  // 1200px
  @if $breakpoint == tab-landt {
    @media (max-width: 75em) {
      @content;
    }
  }

  // NOTE min-width
  // 1800px
  @if $breakpoint == big-desktop {
    @media (min-width: 112.5em) {
      @content;
    }
  }
}


```

base.scss

```
html {
  // NOTE this defines what
  // 1rem is (1rem === 10px); 10px/16px(default px) = 62.5%
  font-size: 62.5%;

  // 56.
  // ORDER OF THE QUERIES MATTER TO WHAT WILL GET APPLIED
  // SET 1 rem to = 9px -> 9/16 = 56.25% (width < 900)
  @include respond(tab-land) {
    font-size: 56.25%;
  }

  // (16 is default font-size) (width < 600)
  // SET 1 rem to = 8px -> 8/16 = 50%
  @include respond(tab-port) {
    font-size: 50%;
  }

  // SET 1 rem to = 12px -> 12/16 = 75%
  @include respond(big-desktop) {
    font-size: 75%;
  }

  // these examples compiles as @include example
  // @media (max-width: 600px) {
  //   font-size: 50%;
  // }

  // @include respond-phone {
  //   font-size: 50%;
  // }
}
```

## 57. Writing Media Queries - Base, Typography and Layout

Order to write media query:
ORDER: Base + typography + general layout + grid > page layout > components

typography.scss

```
  &--main {
    display: block;
    font-size: 6rem;
    font-weight: 400;
    letter-spacing: 3.5rem;

    /* 8. use animation*/
    animation-name: moveInLeft;
    animation-duration: 1s;
    animation-timing-function: ease-out;

    // 57.
    @include respond(phone) {
      letter-spacing: 1rem;
      font-size: 5rem;
    }

      &--sub {
    display: block;
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: 1.74rem;

    animation: moveInRight 1s ease-out;

    @include respond(phone) {
      letter-spacing: 0.5rem;
    }
  }

    // 57.
  @include respond(tab-port) {
    font-size: 3rem;
  }
  @include respond(phone) {
    font-size: 2.5rem;
  }
}
```

grid.scss

```
.row {
  max-width: $grid-width;
  margin: 0 auto;

  &:not(:last-child) {
    margin-bottom: $gutter-vertical;

    @include respond(tab-port) {
      margin-bottom: $gutter-vertical-small;
    }
  }
  // 57. decrease the row width
  @include respond(tab-port) {
    max-width: 50rem;
  }

  @include clearfix;

  // attributes that start with col-
  [class^="col-"] {
    float: left;

    &:not(:last-child) {
      margin-right: $gutter-horizontal;
      // 57. remove gutter since columns turn to rows margin not needed
      @include respond(tab-port) {
        margin-right: 0;
        margin-bottom: $gutter-vertical-small;
      }
    }
    // 57. transform each column to rows. responsive for mobile
    @include respond(tab-port) {
      width: 100% !important;
    }
  }

  .col-1-of-2 {
    width: calc((100% - #{$gutter-horizontal}) / 2);
  }

  .col-1-of-3 {
    width: calc((100% - 2 * #{$gutter-horizontal}) / 3);
  }

  .col-2-of-3 {
    width: calc(
      2 * ((100% - 2 * #{$gutter-horizontal}) / 3) + #{$gutter-horizontal}
    );
  }

  .col-1-of-4 {
    width: calc((100% - 3 * #{$gutter-horizontal}) / 4);
  }

  .col-2-of-4 {
    width: calc(
      2 * ((100% - 3 * #{$gutter-horizontal}) / 4) + #{$gutter-horizontal}
    );
  }

  .col-3-of-4 {
    width: calc(
      3 * ((100% - 3 * #{$gutter-horizontal}) / 4) + 2 * #{$gutter-horizontal}
    );
  }
}

```

what was added:
header.scss

```
.header {
    @include respond(phone) {
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
  }

}
```

Including updated portion:
navigation.scss

```
.navigation {
  &__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    position: fixed;
    top: 6rem;
    right: 6rem;
    border-radius: 50%;
    z-index: 2000;
    box-shadow: 0 1rem 3rem rgba($color-black, 0.1);
    // 51. center the nav button lines
    text-align: center;
    cursor: pointer;

    @include respond(tab-port) {
      top: 4.5rem;
      right: 4.5rem;
    }

    @include respond(tab-port) {
      top: 3.5rem;
      right: 3.5rem;
    }
  }

  &__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;
    // 50. bezier (whip like transition movement)
    transition: transform 0.8s cubic-bezier(0.86, 0, 0.07, 1);
    // transform: scale(80);

    // 57.
    @include respond(tab-port) {
      top: 4.5rem;
      right: 4.5rem;
    }

    @include respond(phone) {
      top: 3.5rem;
      right: 3.5rem;
    }
  }
}
```

footer.scss

```
.footer {
  background-color: $color-grey-dark-3;
  padding: 10rem 0;
  font-size: 1.4rem;
  color: $color-grey-light-1;

  // 57.
  @include respond(tab-port) {
    padding: 8rem 0;
  }

  &__logo-box {
    // image is inline element (behaves like text)
    text-align: center;
    margin-bottom: 8rem;
  }

  &__logo {
    width: 15rem;
    height: auto;
  }

  &__navigation {
    border-top: 1px solid $color-grey-dark-2;
    padding-top: 2rem;
    // shorten the border top length with:
    display: inline-block;

    // 57.
    @include respond(tab-port) {
      width: 100%;
      text-align: center;
    }
  }

  &__list {
    list-style: none;
  }

  &__item {
    display: inline-block;

    &:not(:last-child) {
      margin-right: 1.5rem;
    }
  }

  &__link {
    &:link,
    &:visited {
      color: $color-grey-light-1;
      background-color: $color-grey-dark-3;
      text-decoration: none;
      text-transform: uppercase;
      display: inline-block;
      transition: all 0.2s;
    }

    &:hover,
    &:active {
      color: $color-primary;
      box-shadow: 0 1rem 2rem rgba($color-black, 0.4);
      transform: rotate(5deg) scale(1.3);
    }
  }

  &__copyright {
    border-top: 1px solid $color-grey-dark-2;
    padding-top: 2rem;
    width: 80%;
    float: right;

    // 57.
    @include respond(tab-port) {
      width: 100%;
      float: none;
    }
  }
}

```

## 58. Writing Media Queries - Layout, About and Features Sections

home.scss

```
.section-about {
  background-color: $color-grey-light-1;
  padding: 25rem 0;

  margin-top: -20vh;
  // 58.
  @include respond(tab-port) {
    padding: 20rem 0;
  }
}

// 38.
.section-features {
  padding: 20rem 0;

  background-image: linear-gradient(
      to right bottom,
      rgba($color-primary-light, 0.8),
      rgba($color-primary-dark, 0.8)
    ),
    url(../img/nat-4.jpg);
  background-size: cover;
  transform: skewY(-7deg);

  // raise section to remvove the white polygon shape left from using skew()
  margin-top: -10rem;

  // direct child of selection features, .section-features > *
  & > * {
    transform: skewY(7deg);
  }

  // 58.
  @include respond(tab-port) {
    padding: 15rem 0;
  }
}

// 39.
.section-tours {
  background-color: $color-grey-light-1;
  padding: 25rem 0 15rem 0;
  margin-top: -10rem;

  // 58.
  @include respond(tab-port) {
    padding: 20rem 0 10rem 0;
  }
}

// 42., 43.
.section-stories {
  // padding top/bottom, left/right
  padding: 15rem 0;
  position: relative;

  // 58.
  @include respond(tab-port) {
    padding: 10rem 0;
  }
}

// 45.
.section-book {
  padding: 15rem 0;
  background-image: linear-gradient(
    to right bottom,
    $color-primary-light,
    $color-primary-dark
  ); // 58.
  @include respond(tab-port) {
    padding: 10rem 0;
  }
}

// solid gradient
.book {
  background-image: linear-gradient(
      105deg,
      rgba($color-white, 0.9),
      rgba($color-white, 0.9) 50%,
      transparent 50%
    ),
    url(../../dist/img/nat-10.jpg);
  background-size: 100%;
  border-radius: 3px;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.2);
  height: 50rem;

  &__form {
    width: 50%;
    padding: 6rem;
  }
}

```

utilities.scss

```
.u-margin-bottom-medium {
  margin-bottom: 4rem !important;

  @include respond(tab-port) {
    margin-bottom: 3rem !important;
  }
}

.u-margin-bottom-big {
  margin-bottom: 8rem !important;

  @include respond(tab-port) {
    margin-bottom: 5rem !important;
  }
}

```

composition.scss

```
.composition {
  position: relative;

  &__photo {
    width: 55%;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
    // border-radius: 2px;

    // reference for absolute is 1st parent referenced with set position,
    // i.e top left corner of .composition
    position: absolute;
    z-index: 10;
    transition: all 0.2s 0s;

    outline-offset: 2rem;

    // 58.
    @include respond(tab-port) {
      // float side by side

      float: left;
      position: relative;
      width: 33.3333333%;
      box-shadow: 0 1.5rem 3rem rgba($color-black, 0.2);
    }

    // place images
    &--p1 {
      left: 0;
      top: -2rem;

      // 58.
      @include respond(tab-port) {
        top: 1rem;
        transform: translate(1.2);
      }
    }

    &--p2 {
      right: 0;
      top: 2rem;

      // 58.
      @include respond(tab-port) {
        top: -1rem;
        transform: scale(1.3);
        z-index: 100;
      }
    }

    &--p3 {
      left: 20%;
      top: 10rem;

      // 58.
      @include respond(tab-port) {
        top: 1rem;
        left: 0;
        transform: scale(1.1);
      }
    }

    &:hover {
      outline: 1.5rem solid $color-primary;
      transform: scale(1.05) translateY((-0.5rem));
      box-shadow: 0 2.5rem 4rem rgba($color-black, 0.5);
      z-index: 20;
      border-radius: 0;
    }
  }

  // composition:hover composition__photo:(:hover)
  &:hover & __photo:not(:hover) {
    transform: scale(0.95);
  }
}

```

feature-box.scss

```
// 38.

.feature-box {
  background-color: rgba($color-white, 0.8);
  font-size: 1.5rem;
  padding: 2.5rem;
  text-align: center;
  border-radius: 3px;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

  // 58.
  @include respond(tab-port) {
    padding-inline-start: 2rem;
  }

  // icon
  transition: transform 0.3s;
  &__icon {
    font-size: 6rem;
    margin-bottom: 0.5rem;
    // GRADIANT COLORING
    display: inline-block;
    background-image: linear-gradient(
      to right,
      $color-primary-light,
      $color-primary-dark
    );
    -webkit-background-clip: text;
    color: transparent;

    // 58.
    @include respond(tab-port) {
      margin-bottom: 0;
    }
  }

  &:hover {
    transform: translateY(-1.5rem) scale(1.03);
  }
}

```

## 59. Writing Media Queries - Tours, Stories and Booking Sections

Included the section with the media query
card.scss

```
.card {
  @include respond(tab-port) {
    height: auto;
    border-radius: 3px;
    background-color: $color-white;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &__side {
      height: auto;
      position: relative;

      box-shadow: none;

      &--back {
        transform: rotateY(0);
        // 59.
        clip-path: polygon(0 15%, 100% 0, 100% 100%, 0% 100%);
      }
    }

    &:hover &__side--front {
      transform: rotateY(0);
    }

    &__details {
      padding: 0 1rem;
    }

    // 41. BACK OF CARD STYLING
    &__cta {
      // centering
      position: relative;
      top: 0%;
      left: 00%;
      transform: translate(0);
      width: 100%;
      // 59.
      padding: 7rem 4rem 4em;
    }

    &__price-box {
      margin-bottom: 3rem;
    }

    &__price-only {
      font-size: 1.4rem;
      text-transform: uppercase;
    }

    &__price-value {
      font-size: 4rem;
    }
  }
}
```

story.scss

```
.story {
  width: 75%;
  margin: 0 auto;
  box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
  background-color: rgba($color-white, 60%);
  border-radius: 3px;
  padding: 6rem;
  padding-left: 9rem;
  font-size: $default-font-size;
  transform: skewX(-12deg);

  // 59.
  @include respond(tab-port) {
    width: 100%;
    padding: 4rem;
    padding-left: 7rem;
  }

  @include respond(phone) {
    transform: skew(0);
  }

  &__shape {
    content: " ";
    // start with a square
    width: 15rem;
    height: 15rem;

    float: left;
    // define vectorised shape,
    // element must be floated and have defiened dimensions
    // for shape-outside to work
    // 1st arg radius
    -webkit-shape-outside: circle(50% at 50% 50%);
    shape-outside: circle(50% at 50% 50%);

    // turn square to circle
    -webkit-clip-path: circle(50% at 50% 50%);
    clip-path: circle(50% at 50% 50%);

    // NOTE use transform to move around elements that are floated (better than margin)
    transform: translateX(-3rem) skewX(12deg);
    // 42. make relative for the &__caption position absolute to work
    position: relative;

    // 59.
    @include respond(phone) {
      transform: translateX(-3rem) skew(0);
    }
  }

  // height is 100% of the &__shape width
  &__img {
    // this transition fixed the bug on hover
    // transition did not work after hover state
    transition: transform 0.5s;
    height: 100%;
    transform: translateX(-4rem) scale(1.4);
    backface-visibility: hidden;
  }

  &__text {
    transform: skewX(12deg);
    // 59.
    @include respond(phone) {
      transform: skew(0);
    }
  }

  // position caption dead center
  &__caption {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, 20%);
    color: $color-white;
    text-transform: uppercase;
    font-size: 1.7rem;
    text-align: center;
    opacity: 0;
    transition: all 0.5s;
    // fix shaky glitch
    backface-visibility: hidden;
  }

  &:hover &__caption {
    opacity: 1;
    transform: translate(-50%, -50%);
  }

  &:hover &__img {
    transform: translateX(-4rem) scale(1);
    // filters, blur and reduce brightness (make img darker)
    filter: blur(3px) brightness(80%);
    transition: all 0.5s;
  }
}
```

home.scss

```
.book {
  background-image: linear-gradient(
      105deg,
      rgba($color-white, 0.9) 0%,
      rgba($color-white, 0.9) 50%,
      transparent 50%
    ),
    url(../../dist/img/nat-10.jpg);
  background-size: 100%;
  border-radius: 3px;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.2);

  @include respond(tab-land) {
    background-image: linear-gradient(
        105deg,
        rgba($color-white, 0.9) 0%,
        rgba($color-white, 0.9) 65%,
        transparent 65%
      ),
      url(../../dist/img/nat-10.jpg);
    background-size: cover;
  }

  @include respond(tab-port) {
    background-image: linear-gradient(
        to right,
        rgba($color-white, 0.9) 0%,
        rgba($color-white, 0.9) 100%
      ),
      url(../../dist/img/nat-10.jpg);
    background-size: cover;
  }

  &__form {
    width: 50%;
    padding: 6rem;

    @include respond(tab-land) {
      width: 65%;
    }

    @include respond(tab-port) {
      width: 100%;
    }
  }
}
```

form.scss

```
.form {
  &__group:not(:last-child) {
    margin-bottom: 2rem;
  }

  &__input {
    font-size: 1.5rem;
    // inputs dont inherit font properties by default
    font-family: inherit;
    color: inherit;
    padding: 1.5rem 2rem;
    border-radius: 2px;
    background-color: rgba($color-white, 0.5);
    border: none;
    border-bottom: 3px solid transparent;
    width: 90%;
    display: block;
    transition: all 0.3s;

    // 59.
    @include respond(tab-port) {
      width: 100%;
      margin-bottom: 2rem;
    }

    &:focus {
      outline: none;
      // make element visible to users without a mouse
      box-shadow: 0 1rem 2rem rgba($color-black, 0.1);
      border-bottom: 3px solid $color-primary;
    }

    // when invalid implement this style
    &:focus:invalid {
      border-bottom: 3px solid $color-secondary-dark;
    }

    &::-webkit-input-placeholder {
      color: $color-grey-dark-2;
    }
  }
  &__label {
    font-size: 1.2rem;
    font-weight: 700;
    // display block to use following box properties
    margin-left: 2rem;
    margin-top: 0.7rem;
    display: block;
    transition: all 0.3s;
  }

  // Sibling selector. show text on input
  &__input:placeholder-shown + &__label {
    // possible to animate opacity not visibility
    opacity: 0;
    visibility: hidden;
    transform: translateY(-4rem);
  }

  // 47.
  &__radio-group {
    width: 49%;
    display: inline-block;

    // 59.
    @include respond(tab-port) {
      width: 100%;
      margin-bottom: 2rem;
    }
  }

  // hide radio button
  &__radio-input {
    display: none;
  }

  &__radio-label {
    font-size: $default-font-size;
    cursor: pointer;

    padding-left: 4.5rem;
    position: relative;
  }

  &__radio-button {
    height: 3rem;
    width: 3rem;
    border: 5px solid $color-primary;
    border-radius: 50%;
    display: inline-block;
    position: absolute;
    left: 0;
    top: -0.4rem;

    // inner element circle
    // content and display property must be specified in pseudo elements
    &::after {
      content: "";
      display: block;
      height: 1.3rem;
      width: 1.3rem;
      border-radius: 50%;
      // position circle
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: $color-primary;

      // hide inner circle
      opacity: 0;
      transition: opacicty 0.2s;
    }
  }

  &__radio-input:checked ~ &__radio-label &__radio-button::after {
    opacity: 1;
  }
}
```

## 61. Responsive Images in HTML - Art Direction and Density Switching

- srcset attribute on the <img> and <source>
- <picture> element for Art Direction
- Media quries in HTML

Working on the logo in the footer
Large and small image, one for each screen resolution

footer element:
density switching example
index.html

```
        <img
          srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x"
          alt="Full logo"
          class="footer__logo"
        />
```

Tell browser to use one image on select screen width and another image for other sizes
Art Direction example

```
        <picture class="footer__logo">
          <source
            srcset="
              img/logo-green-small-1x.png 1x,
              img/logo-green-small-2x.png 2x
            "
            media="(max-width: 37.5em)"
          />
          <img
            srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x"
            alt="Full logo"
            class="footer__logo"
            src="img/logo-green-2x.png"
          />
        </picture>
```

## 62. Responsive Images in HTML - Density and Resolution Switching

Working on images in the section about
index.html

```
              <img
                srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"
                sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
                alt="Photo 1"
                class="composition__photo composition__photo--p1"
                src="img/nat-1-large.jpg"
              />
              <img
                srcset="img/nat-2.jpg 300w, img/nat-2-large.jpg 1000w"
                sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
                alt="Photo 2"
                class="composition__photo composition__photo--p2"
                src="img/nat-2-large.j2g"
              />
              <img
                srcset="img/nat-3.jpg 300w, img/nat-3-large.jpg 1000w"
                sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
                alt="Photo 3"
                class="composition__photo composition__photo--p3"
                src="img/nat-3-large.jpg"
              />
```

## 63. Responsive Images in CSS

Using media queries to target resolution

1. Write media query targeting resolution using _min-resolution_
   1. (min-resolution: 920dpi) dots per inch. Spec as per macbook reference
2. Add the alternative photo according to screen resolution

Other responsive changes home.scss

NOTE Convert the px to em: 600/16. Convert px to em in the other responsive changes
header.scss

```
// When resolution greater than 192dpi AND width is larger than 600px then code-block executes

  @media (min-resolution: 192dpi) and (min-width: 600px), (min-width: 2000px) {
    background-image: linear-gradient(
        to right bottom,
        rgba($color-secondary-light, 0.8),
        rgba($color-secondary-dark, 0.8)
      ),
      url(../img/hero-small.jpg);
  }
```

## 64. Testing for Browser Support with @supports

- caniuse.com before using a property in production
- graceful degradation with @supports
- backdrop filter

added prefix for safari compatibilaty
popup.scss

```
  @supports (-webkit-backdrop-filter: blur(10px)) or
    (backdrop-filter: blur(10px)) {
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
    background-color: rgba($color-black, 0.3);
  }
```

added media query and webkit prefix
header.scss

```
  // 63. Responsive images CSS
  // When resolution greater than 192dpi
  // AND width is larger than 600px then code-block executes.
  // logic so the responsive images work on Safari
  @media (min-resolution: 192dpi) and (min-width: 37.5em),
    (min-width: 125em),
    (-webit-min-device-pixel-ratio: 2),
    (min-width: 125em),
    (min-width: 37.5em) {
    background-image: linear-gradient(
        to right bottom,
        rgba($color-secondary-light, 0.8),
        rgba($color-secondary-dark, 0.8)
      ),
      url(../img/hero-small.jpg);
  }

  // if clip-path is supported execute otherwise the height is defaulted to 85vh
    @supports (clip-path: polygon(0 0)) or (-webkit-clip-path: polygon(0 0)) {
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
    height: 95vh;
  }
```

or vs and

- you use "or" keyword only inside @supports at-rule (if you type comma instead, vs code will actually highlight it as an error)
- if you have to add "or" logic inside @media - you use comma

## 65. Setting up a Simple Build Process with NPM Scripts

- npm concat. To use run the script in the package.json
- npm i autoprefixer
- npm i postcss-cli, npm i postcss --save-dev. needed for autoprefixer to work
- npm i npm-run-all

1. watch sass file, output to dist/css/style.css
2. compile the sass, output to dist/css/style.comp.css
3. concat the files: npm run concat:css
4. prefix:css

```
  "scripts": {
    "watch:sass": "sass --watch --update sass/main.scss dist/css/style.css -w",
    "devserver": "live-server --open=dist/index.html",
    "start": "npm-run-all --parallel devserver watch:sass",
    "compile:sass": "sass sass/main.scss dist/css/style.comp.css",
    "concat:css": "concat -o dist/css/style.concat.css dist/css/icon-font.css dist/css/style.comp.css",
    "prefix:css": "postcss --use autoprefixer -b 'last 10 version' dist/css/style.concat.css -o dist/css/style.prefix.css ",
    "compress:css": "sass dist/css/style.prefix.css dist/css/style.css  --style=compressed",
    "build:css": "npm-run-all compile:sass concat:css prefix:css compress:css"
  },
```

```
  "devDependencies": {
    "autoprefixer": "^10.4.13",
    "concat": "^1.0.3",
    "npm-run-all": "^4.1.5",
    "postcss": "^8.4.21",
    "sass": "^1.58.0"
  },
  "dependencies": {
    "postcss-cli": "^10.1.0"
  }
```

## 66. Wrapping up the Natours Project: Final Considerations

Change style on selected text

base.scss

```
::selection {
  background-color: $color-primary;
  color: $color-white;
}
```

updated media queries so queries apply to screens only not print jobs

```
  @if $breakpoint == phone {
    @media only screen and (max-width: 37.5em) {
      @content;
    }
  }
```

updated to have a media query instead of mixin so we could add the 2nd argument of only screen
Showing the price of the tour on touch devices
card.scss

```
// @include respond(tab-port) {
  @media only screen and (max-width: 56.25em), only screen and (hover: none) {
    height: auto;
    border-radius: 3px;
    background-color: $color-white;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &__side {
      height: auto;
      position: relative;

      box-shadow: none;

      &--back {
        transform: rotateY(0);
        // 59.
        clip-path: polygon(0 15%, 100% 0, 100% 100%, 0% 100%);
      }
    }

    &:hover &__side--front {
      transform: rotateY(0);
    }

    &__details {
      padding: 0 1rem;
    }

    // 41. BACK OF CARD STYLING
    &__cta {
      // centering
      position: relative;
      top: 0%;
      left: 00%;
      transform: translate(0);
      width: 100%;
      // 59.
      padding: 7rem 4rem 4em;
    }

    &__price-box {
      margin-bottom: 3rem;
    }

    &__price-only {
      font-size: 1.4rem;
      text-transform: uppercase;
    }

    // 59. FONT SIZE
    &__price-value {
      font-size: 4rem;
    }
  }
```
