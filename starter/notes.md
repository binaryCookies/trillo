VSCODE
CTRL+PgUp to previous tab and CTRL+PgDown to next tab.

## 68.

- Flexbox give container the ability to expand and shrink elements to best sut available space (replace float layouts)
- 1 dimensional layouts use flexbox, 2D better to use CSS Grid
- Element in which use flexbox is the : flex container
- Direct children of the flexbox container known as: flex-items
- Main axis: example horizontal
- Cross axis: example vertical axis

Properties Overview
CONTANER

1. Flex direction: row | row-reverse | coluum | column-reverse
2. Flex-wrap: nowrap | wrap | wrap-reverse
3. justify-content (important to know where the main axis is):
4. align-items (aligns along cross axis):
5. align-content when more than one row flex items

ITEM

1. align-self: use case if align-items is set to center but we want an item to have differct behaviour we use align-self
2. order: defines order of one specific flex item should appear inside the container
3. flex-grow: 0 | <integer> define how much an item can grow
4. flex-shrink: 1 | <integer> define how much an item can shrink
5. flex-basis: auto | length define blase width
6. flex: shorthand for numbers 3,4,5
   1. flex: 0 1 auto

## 69.

Tip: small screens set the flex-direciton to column so items will appear one on top of the other

Align-items: baseline will align according to the text not the axis

flex-direction, justify-content, align-items most frequently used

important to know where the main axis is when using flex-direction and justify-content

## 70. A Basic Intro to Flexbox: Flex Items

https://codepen.io/litonfiredesign/full/OaZLWd

Testing the flex container and item properties

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  background-color: #ccc;
  padding: 10px;

  display: flex;
  /*row, column, row, row-reverse, column-reverse */
  flex-direction: row;

/* how items appear on the main axis: space-between,  space-around space at start and end 1/2 width, space evenly, flex-end, flex-start, center*/
  justify-content: space-between;

/*using cross axis: baseline, flex-start, flex-end    */
  align-items: center;
}

.item {
  background-color: #f1254d;
  padding: 30px;
  margin: 30px;
  color: #fff;
  font-size: 40px;

  flex-grow: 1;
}

.i2 {
  font-size: 30px;
  height: 200px;
  order:1;

/*  integer used relative to other integers used with flex-grow property -shorthand flex: 2  */
  flex-grow: 2;

/*  control width  */
  flex-basis: 300px

/*  prevent shrinking with 0
    flex-shrink:0; */
  flex: 0 1 300px;
}

.i4 {
  font-size: 70px;
/*  overwrite align-items:center  */
  align-self: flex-end;

/*  initial value is 0    */
    order: -1;
}
```

```
<div class=container>
  <div class="item">1</div>
  <div class="item i2">2</div>
  <div class="item">3</div>
  <div class="item i4">4</div>
  <div class="item">5</div>
</div>
```

## 71. A Basic Intro to Flexbox: Adding More Flex Items

kept the changes to be able to see the different effects as seen in the video instruction

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  background-color: #ccc;
  padding: 10px;

  display: flex;
  flex-direction: row;


  justify-content: space-between;

  align-items: center;

/*   71. align content aligns along cross axis, used to remove whitespace between rows*/
  flex-wrap: wrap;
  height: 1000px;
  align-content: flex-start;
}

.item {
  background-color: #f1254d;
  padding: 30px;
  margin: 5px;
  color: #fff;
  font-size: 40px;

}

.i2 {
  font-size: 30px;
  height: 200px;
  order:1;

  flex-grow: 2;

  flex-basis: 300px
  flex: 0 1 300px;
}

.i4 {
  font-size: 70px;
  //align-self: flex-end;

/*  initial value is 0    */
    order: -1;
}
```

## 72.

refresher of the build scripts
development portion
package.json

```
    "watch:sass": "sass --watch --update sass/main.scss css/style.css -w",
    "devserver": "live-server --open=index.html",
    "start": "npm-run-all --parallel devserver watch:sass",

```

build portion

```
   "compile:sass": "sass sass/main.scss css/style.comp.css",
    "prefix:css": "postcss --use autoprefixer -b 'last 10 version'  -o css/style.prefix.css ",
    "compress:css": "sass css/style.prefix.css css/style.css  --style=compressed",
    "build:css": "npm-run-all compile:sass prefix:css compress:css"

```

## 73. Defining Project Settings and Custom Properties

How and why to use CSS custom properties istead of sass variables

- global reset with global box-sizing
- custom CSS properties/variables
- margin settings,
- setting global font size
- background gradient
- font definitions (google fonts)

```
:root {
  --color-primary: #eb2f64;
  --color-primary-light: #ff3366;
  --color-primary-dark: #ba265d;

  --color-grey-light-1: #faf9f9;
  --color-grey-light-2: #f4f2f2;
  --color-grey-light-3: #f0eeee;
  --color-grey-light-4: #ccc;

  --color-grey-dark-1: #333;
  --color-grey-dark-2: #777;
  --color-grey-dark-3: #999;
}

* {
  margin: 0;
  padding: 0;
}

// 73.
*,
*::before,
*::after {
  box-sizing: inherit;
}

html {
  box-sizing: border-box;
  font-size: 62.5%; // 1 rem = 10px, 10px/16px = 62.5%
}

body {
  font-family: "Open Sans", sans-serif;
  font-weight: 400;
  line-height: 1.6;
  color: var(--color-grey-dark-2);
  background-image: linear-gradient(
    to right bottom,
    var(--color-primary-light),
    var(--color-primary-dark)
  );
  background-size: cover;
  background-repeat: no-repeat;

  // height was following text so we increased it
  min-height: 100vh;
}
```

## 74. Building the Overall Layout

Initialized the layout for the sidebar, header, content and hotel-view sections

index.html

```
<body>
    <div class="container">
      <header class="header">Header Part</header>
      <div class="content">
        <nav class="sidebar">Navigation</nav>
        <main class="hotel-view">Hotel view</main>
      </div>
    </div>
  </body>
```

layout.scss

```
.container {
  max-width: 120rem;
  margin: 8rem auto;
  background-color: var(--color-grey-light-2);
  box-shadow: var(--shadow-dark);

  min-height: 50rem;
}

.header {
  height: 7rem;
  background-color: #fff;
  border-bottom: var(--color-grey-light-2);
}

.content {
  display: flex;
}

.sidebar {
  background-color: var(--color-grey-dark-1);
  // grow shrink basis
  flex: 0 0 18%;
}

.hotel-view {
  background-color: #fff;
  background-color: orangered;
  flex: 1;
}

```

## 75. Building the Header - Part 1

icoMoon.io: convert icon fonts to svg or download free icons
dowloaded icons from the site and saved to img folder the SVG folder and symbol-defs renamed it to sprite

include the svg in html with svg sprites
Header Markup
index.html

```
  <body>
    <div class="container">
      <header class="header">
      <img src="img/logo.png" alt="trillo logo" class="logo" />

      <form action="#" class="search">
        <input type="text" class="search__input" placeholder="Search hotels" />
        <button class="search__button">
          <svg class="search__icon">
            <use href="img/sprite.svg#icon-magnifying-glass"></use>
          </svg>
        </button>
      </form>

      <nav class="user-nav">
        <div class="user-nav__icon-box">
          <svg class="user-nav__icon">
            <use href="img/sprite.svg#icon-icon-bookmark"></use>
          </svg>
          <span class="user-nav__notification">7</span>
        </div>

        <div class="user-nav__icon-box">
          <svg class="user-nav__icon">
            <use href="img/sprite.svg#icon-chat"></use>
          </svg>
          <span class="user-nav__notification">13</span>
        </div>

        <div class="user-nave__user">
          <img
            src="img/user.jpg"
            alt="user photo"
            class="user-nav__user-photo"
          />
        <span class="user-nav__user-name">Jonas</span>
        </div>
      </nav>
    </header>
      <div class="content">
        <nav class="sidebar">Navigation</nav>
        <main class="hotel-view">Hotel view</main>
      </div>
    </div>
  </body>
```

Including the SVG's
components.scss

```
// LOGO
.logo {
  height: 3.25rem;
}
////////////////////////////////////////
// SEARCH
.search {
  &__input {
  }

  &__button {
  }

  &__icon {
    height: 2rem;
    width: 2rem;
  }
}
////////////////////////////////////////
// USER NAVIGATION
.user-nav {
  &__icon-box {
  }

  &__icon {
    height: 2.25rem;
    width: 2.25rem;
  }

  &__notification {
  }

  &__user {
  }

  &__user-photo {
    height: 3.75rem;
    border-radius: 50%;
  }

  &__user-name {
  }
}
```

## 76. Building the Header - Part 2

added a background image to visualize the boxes/layouts
aligned svg icons n the header along main axis and cross axis i

layout.scss

```
.header {
  height: 7rem;
  background-color: #fff;
  border-bottom: var(--color-grey-light-2);

  display: flex;
  // 76. align along main axis
  justify-content: space-between;
  // align along cross axis
  align-items: center;
}
```

Updates to the following components:
logo
search
button
components.scss

```
// LOGO
.logo {
height: 3.25rem;
margin-left: 3rem;
}
////////////////////////////////////////
// SEARCH
.search {
// 76.
flex: 0 0 40%;

// align magnifying glass in the search bar
// nested flex-box , item given flex container property
display: flex;
align-items: center;
justify-content: center;

&\_\_input {
font-family: inherit;
font-size: inherit;
color: inherit;
background-color: var(--color-grey-light-2);
border: none;
padding: 0.7rem 2rem;
border-radius: 100px;
width: 90%;
transition: all 0.2s;
// trick to move button on top of the input bar
margin-right: -3.25rem;

    &:focus {
      outline: none;
      width: 100%;
      background-color: var(--color-grey-light-3);
    }

    // change placeholder text
    &::-webkit-input-placeholder {
      font-weight: 100;
      color: var(--color-grey-light-4);
    }

}

// adjacent selector (for siblings)
&**input:focus + &**button {
background-color: var(--color-grey-light-3);
}

&\_\_button {
border: none;
background-color: var(--color-grey-light-2);

    &:focus {
      outline: none;
    }

    &:active {
      transform: translateY(2px);
    }

}

&**icon {
height: 2rem;
width: 2rem;
// change svg color
fill: var(--color-grey-dark-3);
}
}
////////////////////////////////////////
// USER NAVIGATION
.user-nav {
background-color: greenyellow;
&**icon-box {
}

&\_\_icon {
height: 2.25rem;
width: 2.25rem;
}

&\_\_notification {
}

&\_\_user {
}

&\_\_user-photo {
height: 3.75rem;
border-radius: 50%;
}

&\_\_user-name {
}
}

```

### Why we use px here for border-radius instead of % ?

So, we use px and % in different situations. We use percentages more for "layout" elements, which means elements that define the layout and that we want to change according to the screen width. Also, percentages are most useful for defining horizontal distances between elements, such as widths or margin-left or margin-right, not vertical distances, because responsive web design works with screen widths (horizontal). In other words, everything that we want to change based on the screen width when the screen becomes smaller, should be defined in %.

Also, font-sizes are always defined in %, except for the base font-size defined for the body element, so that we can easily change font-sizes for smaller screen sizes. There is more about this later in Section 6 of the course.

We use px to define some margins and paddings, and sometimes to define smaller distances and distances that don’t need to change when the screen changes. For the paddings, please note that we can only use px thanks to box-sizing: border-box; , which ensures that the box width (defined in %) always stays the same no matter how much padding we add inside of it.

## 77. Building the Header - Part 3

User navigation
nested flex containers, using item/elements as flex containers

Styled all components in the header section
components.scss

```
////////////////////////////////////////
// LOGO
.logo {
  height: 3.25rem;
  margin-left: 2rem;
}
////////////////////////////////////////
// SEARCH
.search {
  // 76.
  flex: 0 0 40%;

  // align magnifying glass in the search bar
  // nested flex-box , item given flex container property
  display: flex;
  align-items: center;
  justify-content: center;

  &__input {
    font-family: inherit;
    font-size: inherit;
    color: inherit;
    background-color: var(--color-grey-light-2);
    border: none;
    padding: 0.7rem 2rem;
    border-radius: 100px;
    width: 90%;
    transition: all 0.2s;
    // trick to move button on top of the input bar
    margin-right: -3.25rem;

    &:focus {
      outline: none;
      width: 100%;
      background-color: var(--color-grey-light-3);
    }

    // change placeholder text
    &::-webkit-input-placeholder {
      font-weight: 100;
      color: var(--color-grey-light-4);
    }
  }

  // adjacent selector (for siblings)
  &__input:focus + &__button {
    background-color: var(--color-grey-light-3);
  }

  &__button {
    border: none;
    background-color: var(--color-grey-light-2);

    &:focus {
      outline: none;
    }

    &:active {
      transform: translateY(2px);
    }
  }

  &__icon {
    height: 2rem;
    width: 2rem;
    // change svg color
    fill: var(--color-grey-dark-3);
  }
}
////////////////////////////////////////
// USER NAVIGATION
.user-nav {
  align-self: stretch;
  display: flex;
  align-items: center;

  // select direct children of .user-nav
  & > * {
    padding: 0 2rem;
    cursor: pointer;
    height: 100%;
    display: flex;
    align-items: center;
  }

  & > *:hover {
    background-color: var(--color-grey-light-2);
  }

  &__icon-box {
    position: relative;
  }

  &__icon {
    height: 2.25rem;
    width: 2.25rem;
    fill: var(--color-grey-dark-2);
  }

  &__notification {
    font-size: 0.8rem;
    height: 1.75rem;
    width: 1.75rem;
    border-radius: 50%;
    background-color: var(--color-primary);
    color: #fff;

    // Placement
    position: absolute;
    top: 1.5rem;
    right: 1.1rem;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__user-photo {
    height: 3.75rem;
    border-radius: 50%;
    margin-right: 1rem;
  }
}

```

## 78. Building the Navigation - Part 1 & 79. Building the Navigation - Part 2

- scaleY & multiple transtion properties to create hover effect
- About the currentColor CSS variable
- Advance alignment techniques with flexbox: flex-direction, justify-content, align-items

changed the flex direction of the sidebar nav and use space-between to space out elements so legal text is at the bottom and nav at the top.
layout.scss

```
.sidebar {
  background-color: var(--color-grey-dark-1);

  // grow shrink basis
  flex: 0 0 18%;

  // placing legal text at bottom of page
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
```

Added the updates
components.scss

```
////////////////////////////////////////
// 78. USER NAVIGATION
.user-nav {
  align-self: stretch;
  display: flex;
  align-items: center;

  // select direct children of .user-nav
  & > * {
    padding: 0 2rem;
    cursor: pointer;
    height: 100%;
    display: flex;
    align-items: center;
  }

  & > *:hover {
    background-color: var(--color-grey-light-2);
  }

  &__icon-box {
    position: relative;
  }

  &__icon {
    height: 2.25rem;
    width: 2.25rem;
    fill: var(--color-grey-dark-2);
  }

  &__notification {
    font-size: 0.8rem;
    height: 1.75rem;
    width: 1.75rem;
    border-radius: 50%;
    background-color: var(--color-primary);
    color: #fff;

    // Placement
    position: absolute;
    top: 1.5rem;
    right: 1.1rem;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__user-photo {
    height: 3.75rem;
    border-radius: 50%;
    margin-right: 1rem;
  }
}

////////////////////////////////////////
// SIDE NAVIGATION
.side-nav {
  font-size: 1.4rem;
  list-style: none;
  margin-top: 3.5rem;

  &__item {
    position: relative;

    &:not(:last-child) {
      margin-bottom: 0.5rem;
    }
  }

  &__item::before {
    content: "";
    position: absolute;
    top: 0;
    height: 100%;
    width: 3px;
    background-color: var(--color-primary);
    transform: scaleY(0);

    //transform-origin: bottom;
    // add delay to transfor width
    transition: transform 0.2s, width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s,
      background-color 0.1s;
  }

  &__item:hover::before,
  &__item--active::before {
    transform: scaleY(1);
    width: 100%;
  }

  // make button brighter color to show active state
  &__item:active::before {
    background-color: var(--color-primary-light);
  }

  &__link:link,
  &__link:visited {
    color: var(--color-grey-light-1);
    text-decoration: none;
    text-transform: uppercase;
    display: block;
    padding: 1.5rem 3rem;
    position: relative;
    z-index: 10;

    display: flex;
    align-items: center;
  }

  //   &__link:hover {
  //     color: orangered;
  //   }

  &__icon {
    width: 1.75rem;
    height: 1.75rem;
    margin-right: 2rem;
    fill: currentColor;
  }
}

////////////////////////////////////////
// LEGAL TEXT

.legal {
  font-size: 1.2rem;
  text-align: center;
  color: --color-grey-dark-4;
  padding: 2.5rem;
}

```

## 80. Building the Hotel Overview - Part 1

- Create infinite animation
- How to use margin: auto with flexbox, very powerful
- flexbox properties for easy positioning and alignment

NOTE GREAT TRICK: use margin auto to add space without stretching out element to occupy more space than the content. This is important for things like hovering.

conponents.scss

```
  &__stars {
    margin-right: auto;
  }
```

HOTEL OVERVIEW

```
.overview {
  display: flex;

  &__heading {
  }

  &__stars {
    margin-right: auto;
  }

  &__icon-star,
  &__icon-location {
    width: 1.75rem;
    height: 1.75rem;
    fill: var(--color-primary);
  }

  &__location {
  }

  &__rating {
  }

  &__rating-average {
  }

  &__rating-count {
  }
}
```

## 81. Building the Hotel Overview - Part 2

```
// HOTEL OVERVIEW
.overview {
  display: flex;
  align-items: center;
  border-bottom: 1px solid var(--color-grey-light-2);

  &__heading {
    font-size: 2.25rem;
    font-weight: 300;
    text-transform: uppercase;
    letter-spacing: 1px;
    padding: 1.5rem 3rem;
  }

  &__stars {
    margin-right: auto;
    // remove the whitespace caused by svg as they
    // behave like text and leave a small whitespace at the bottom
    display: flex;
  }

  &__icon-star,
  &__icon-location {
    width: 1.75rem;
    height: 1.75rem;
    fill: var(--color-primary);
  }

  &__location {
    font-size: 1.2rem;
    display: flex;
    vertical-align: center;
  }

  &__icon-location {
    margin-right: 0.5rem;
  }

  &__rating {
    background-color: var(--color-primary);
    color: #fff;
    margin-left: 3rem;
    padding: 0 2.25rem;
    align-self: stretch;

    flex-direction: column;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__rating-average {
    font-size: 2.25rem;
    font-weight: 300;
    margin-bottom: -3px;
  }

  &__rating-count {
    font-size: 0.8rem;
    text-transform: uppercase;
  }
}

////////////////////////////////////////
// BUTTON INLINE
.btn-inline {
  border: none;
  color: var(--color-primary);
  font-size: inherit;
  border-bottom: 1px solid currentColor;
  padding-bottom: 2px;
  display: inline-block;
  background-color: transparent;
  cursor: pointer;
  transition: all 0.2s;

  &:hover {
    color: var(--color-grey-dark-1);
  }

  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

@keyframes pulsate {
  0% {
    transform: scale(1);
    box-shadow: none;
  }

  50% {
    transform: scale(1.05);
    box-shadow: 0 1rem 4rem rgba(0, 0, 0, 0.25);
  }

  100% {
    transform: scale(1);
    box-shadow: none;
  }
}
```

## 82. Building the Description Section - Part 1

CSS masks with mask-image and mask-size

layout.scss

```
.hotel-view {
  //background-color: #fff;

  flex: 1;
}

.detail {
  display: flex;
  padding: 4.5rem;
  background-color: var(--color-grey-light-1);
  border-bottom: var(--line);
}

.description {
  font-size: 1.4rem;
  background-color: #fff;
  box-shadow: var(--shadow-light);
  padding: 3rem;
  flex: 0 0 60%;
  margin-right: 4.5rem;
}

.user-reviews {
  background-color: yellowgreen;
  flex: 1;
}
```

index.html

```
<div class="detail">
            <div class="description">
              <p class="paragraph">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi
                nisi dignissimos debitis ratione sapiente saepe. Accusantium
                cumque, quas, ut corporis incidunt deserunt quae architecto
                voluptate.
              </p>
              <p class="paragraph">
                Accusantium cumque, quas, ut corporis incidunt deserunt quae
                architecto voluptate delectus, inventore iure aliquid aliquam.
              </p>
              <ul class="list">
                <li class="list__item">Close to the beach</li>
                <li class="list__item">Breakfast included</li>
                <li class="list__item">Free airport shuttle</li>
                <li class="list__item">Free wifi in all rooms</li>
                <li class="list__item">Aircontioning and heatings</li>
                <li class="list__item">Pets allowed</li>
                <li class="list__item">We speak all languages</li>
                <li class="list__item">Perfect for families</li>
              </ul>
              <div class="recommend">
                <p class="recommend__count">
                  Lucy and 3 other friends recommend this hotel.
                </p>
                <div class="recommend__friends">
                  <img
                    src="img/user-1.jpg"
                    alt="Friend 1"
                    class="recommend__photo"
                  />
                  <img
                    src="img/user-2.jpg"
                    alt="Friend 2"
                    class="recommend__photo"
                  />
                  <img
                    src="img/user-3.jpg"
                    alt="Friend 3"
                    class="recommend__photo"
                  />
                  <img
                    src="img/user-4.jpg"
                    alt="Friend 4"
                    class="recommend__photo"
                  />
                </div>
              </div>
            </div>

            <div class="user-reviews">User reviews</div>
          </div>
```

## 83. Building the Description Section - Part 2

- flex-wrap
- masks
- margin-right: auto;

components.scss

```
////////////////////////////////////////
// PARAGRAPH
.paragraph:not(:last-of-type) {
  margin-bottom: 2rem;
}

////////////////////////////////////////
// LIST
.list {
  list-style: none;
  margin: 3rem 0;
  padding: 3rem 0;
  border-top: var(--line);
  border-bottom: var(--line);

  display: flex;
  flex-wrap: wrap;

  &__item {
    flex: 0 0 50%;
    margin-bottom: 0.7rem;
  }

  // NOTE 83. TIP TO CHANGE THE COLOR OF THE SVG ICON
  &__item::before {
    content: "";
    display: inline-block;
    height: 1rem;
    width: 1rem;
    margin-right: 0.7rem;
    // older browsers
    // background-image: url(../img/chevron-thin-right.svg);
    // background-size: cover;

    // Newer Browsers - masks
    background-color: var(--color-primary);
    -webkit-mask-image: url(../img/chevron-thin-right.svg);
    -webkit-mask-size: cover;
    mask-image: url(../img/chevron-thin-right.svg);
    mask-size: cover;
  }
}

////////////////////////////////////////
// 83. RECOMMEND
.recommend {
  font-size: 1.3rem;
  color: var(--color-grey-dark-3);

  display: flex;
  align-items: center;

  &__count {
    margin-right: auto;
  }

  &__friends {
  }

  &__photo {
    // prevent border from shrinking size of photo with content-box
    box-sizing: content-box;
    height: 4rem;
    width: 4rem;
    border-radius: 50%;
    border: 3px solid #fff;

    &:not(:last-child) {
      margin-right: -1.5rem;
    }
  }
}

```

## 84. Building the User Reviews Section

layout.scss

```
.user-reviews {
  flex: 1;

  // 84.
  display: flex;
  flex-direction: column;
  align-items: center;
}
```

styling of the user reviews
entity code for CSS
Use of margin-right: auto

components.scss

```
// BUTTON INLINE
.btn-inline {
  border: none;
  color: var(--color-primary);
  font-size: inherit;
  border-bottom: 1px solid currentColor;
  padding-bottom: 2px;
  display: inline-block;
  background-color: transparent;
  cursor: pointer;
  transition: all 0.2s;

  // 84.
  & span {
    margin-left: 3px;
    transition: margin-left 0.2s;
  }

  &:hover {
    color: var(--color-grey-dark-1);

    span {
      margin-left: 8px;
    }
  }

  // Animate
  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

// 83. RECOMMEND
.recommend {
  font-size: 1.3rem;
  color: var(--color-grey-dark-3);

  display: flex;
  align-items: center;

  &__count {
    margin-right: auto;
  }

  &__friends {
  }

  &__photo {
    // prevent border from shrinking size of photo with content-box
    box-sizing: content-box;
    height: 4rem;
    width: 4rem;
    border-radius: 50%;
    border: 3px solid #fff;

    &:not(:last-child) {
      margin-right: -1.5rem;
    }
  }
}

////////////////////////////////////////
// 84. REVIEWS
.review {
  background-color: #fff;
  box-shadow: var(--shadow-light);
  padding: 3rem;
  margin-bottom: 3.5rem;
  position: relative;
  overflow: hidden;

  &__text {
    margin-bottom: 2rem;

    // z-index only works if position is set
    z-index: 10;
    position: relative;
  }

  &__user {
    display: flex;
    align-items: center;
  }

  &__photo {
    height: 4.5rem;
    width: 4.5rem;
    border-radius: 50%;
    margin-right: 1.5rem;
  }

  &__user-box {
    // gives margin between user-name, user-date from user-rating
    margin-right: auto;
  }

  &__user-name {
    font-size: 1.1rem;
    font-weight: 600;
    text-transform: uppercase;
    margin-bottom: 0.4rem;
  }

  &__user-date {
    font-size: 1rem;
    color: var(--color-grey-dark-3);
  }

  &__rating {
    color: var(--color-primary);
    font-size: 2.2rem;
    font-weight: 300;
  }

  &::before {
    // entity code for quotation marks, from CSStricks.com
    content: "\201C";
    position: absolute;
    top: -2.75rem;
    left: -1rem;
    line-height: 1;
    font-size: 20rem;
    color: var(--color-grey-light-2);
    font-family: sans-serif;
    z-index: 1;
  }
}
```

user-reviews section, corrected and added markup
index.html

```
            <div class="user-reviews">
              <figure class="review">
                <blockquote class="review__text">
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Fuga
                  doloremque architecto dicta animi, totam, itaque officia ex.
                </blockquote>
                <figcaption class="review__user">
                  <img src="img/user-1.jpg" alt="" class="review__photo" />
                  <div class="review__user-box">
                    <p class="review__user-name">Nick Smith</p>
                    <p class="review__user-date">Feb 23rd, 2023</p>
                  </div>
                  <div class="review__rating">7.8</div>
                </figcaption>
              </figure>

              <figure class="review">
                <blockquote class="review__text">
                  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Fuga
                  doloremque architecto dicta animi.
                </blockquote>
                <figcaption class="review__user">
                  <img src="img/user-2.jpg" alt="" class="review__photo" />
                  <div class="review__user-box">
                    <p class="review__user-name">Mary Thomas</p>
                    <p class="review__user-date">Sept 13th, 2022</p>
                  </div>
                  <div class="review__rating">9.3</div>
                </figcaption>
              </figure>

              <button class="btn-inline">Show all <span>&rarr;</span></button>
            </div>
```

## 85. Building the CTA Section

call to action
component.scss

```
////////////////////////////////////////
// 85. CALL TO ACTION
.cta {
  padding: 3.5rem 0;
  text-align: center;

  &__book-now {
    font-size: 2rem;
    font-weight: 300;
    text-transform: uppercase;
    margin-bottom: 2.5rem;
  }
}

////////////////////////////////////////
// 85. CALL TO ACTION
.btn {
  font-size: 1.5rem;
  font-weight: 300;
  text-transform: uppercase;
  border-radius: 100px;
  border: none;
  background-image: linear-gradient(
    to right,
    var(--color-primary-light),
    var(--color-primary-dark)
  );
  color: #fff;
  position: relative;
  //hide the text that is outside the book now button
  overflow: hidden;
  cursor: pointer;

  & > * {
    display: inline-block;
    height: 100%;
    width: 100%;
    transition: all 0.2s;
  }

  &__visible {
    //inline block to use padding
    padding: 2rem 7.5rem;
  }

  &__invisible {
    position: absolute;
    padding: 2rem 0;
    left: 0;
    top: -100%;
  }

  &:hover {
    background-image: linear-gradient(
      to left,
      var(--color-primary-light),
      var(--color-primary-dark)
    );
  }

  &:hover &__visible {
    // we dont use top property because
    // we did not set position to absolute on it
    transform: translateY(100%);
  }

  &:hover &__invisible {
    top: 0;
  }

  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}
```

index.html

```
          <!-- 85 CTA: CALL TO ACTION-->
          <div class="cta">
            <h2 class="cta__book-now">
              Good news! We have 4 free rooms for your selected dates
            </h2>
            <button class="btn">
              <span class="btn__visible">Book now</span>
              <span class="btn__invisible">Only 4 rooms left</span>
            </button>
          </div>
```

## 86. Writing Media Queries - Part 1

breakpoints
base.scss

```
$bp-largest: 75em; // 1200px
$bp-large: 68.75em; // 1100px
$bp-medium: 56.25em; // 900px
```

media queries responsiveness
layout.scss

```

.container {
max-width: 120rem;
margin: 8rem auto;
background-color: var(--color-grey-light-2);
box-shadow: var(--shadow-dark);

min-height: 50rem;

@media only screen and (max-width: $bp-largest) {
margin: 0;
max-width: 100%;
width: 100%;
}
}

.content {
display: flex;
@media only screen and (max-width: $bp-medium) {
flex-direction: column;
}
}

.detail {
font-size: 1.4rem;
display: flex;
padding: 4.5rem;
background-color: var(--color-grey-light-1);
border-bottom: var(--line);

// 86.
@media only screen and (max-width: $bp-medium) {
padding: 3rem;
}
}

.description {
// NOTE font-size is inherited from parent element
background-color: #fff;
box-shadow: var(--shadow-light);
padding: 3rem;
flex: 0 0 60%;
margin-right: 4.5rem;

@media only screen and (max-width: $bp-medium) {
padding: 2rem;
margin-right: 3rem;
}
}

```

components.scss

```
////////////////////////////////////////
// LOGO
.logo {
  height: 3.25rem;
  margin-left: 2rem;
}
////////////////////////////////////////
// SEARCH
.search {
  // 76.
  flex: 0 0 40%;

  // align magnifying glass in the search bar
  // nested flex-box , item given flex container property
  display: flex;
  align-items: center;
  justify-content: center;

  &__input {
    font-family: inherit;
    font-size: inherit;
    color: inherit;
    background-color: var(--color-grey-light-2);
    border: none;
    padding: 0.7rem 2rem;
    border-radius: 100px;
    width: 90%;
    transition: all 0.2s;
    // trick to move button on top of the input bar
    margin-right: -3.25rem;

    &:focus {
      outline: none;
      width: 100%;
      background-color: var(--color-grey-light-3);
    }

    // change placeholder text
    &::-webkit-input-placeholder {
      font-weight: 100;
      color: var(--color-grey-light-4);
    }
  }

  // adjacent selector (for siblings)
  &__input:focus + &__button {
    background-color: var(--color-grey-light-3);
  }

  &__button {
    border: none;
    background-color: var(--color-grey-light-2);

    &:focus {
      outline: none;
    }

    &:active {
      transform: translateY(2px);
    }
  }

  &__icon {
    height: 2rem;
    width: 2rem;
    // change svg color
    fill: var(--color-grey-dark-3);
  }
}
////////////////////////////////////////
// 78. USER NAVIGATION
.user-nav {
  align-self: stretch;
  display: flex;
  align-items: center;

  // select direct children of .user-nav
  & > * {
    padding: 0 2rem;
    cursor: pointer;
    height: 100%;
    display: flex;
    align-items: center;
  }

  & > *:hover {
    background-color: var(--color-grey-light-2);
  }

  &__icon-box {
    position: relative;
  }

  &__icon {
    height: 2.25rem;
    width: 2.25rem;
    fill: var(--color-grey-dark-2);
  }

  &__notification {
    font-size: 0.8rem;
    height: 1.75rem;
    width: 1.75rem;
    border-radius: 50%;
    background-color: var(--color-primary);
    color: #fff;

    // Placement
    position: absolute;
    top: 1.5rem;
    right: 1.1rem;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__user-photo {
    height: 3.75rem;
    border-radius: 50%;
    margin-right: 1rem;
  }
}

////////////////////////////////////////
// SIDE NAVIGATION
.side-nav {
  font-size: 1.4rem;
  list-style: none;
  margin-top: 3.5rem;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    display: flex;
    margin: 0;
  }

  &__item {
    position: relative;

    &:not(:last-child) {
      margin-bottom: 0.5rem;

      // 86.
      @media only screen and (max-width: $bp-medium) {
        margin: none;
      }
    }
    // 86.
    @media only screen and (max-width: $bp-medium) {
      flex: 1;
    }
  }

  &__item::before {
    content: "";
    position: absolute;
    top: 0;
    height: 100%;
    width: 3px;
    background-color: var(--color-primary);
    transform: scaleY(0);

    //transform-origin: bottom;
    // add delay to transfor width
    transition: transform 0.2s, width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s,
      background-color 0.1s;
  }

  &__item:hover::before,
  &__item--active::before {
    transform: scaleY(1);
    width: 100%;
  }

  // make button brighter color to show active state
  &__item:active::before {
    background-color: var(--color-primary-light);
  }

  &__link:link,
  &__link:visited {
    color: var(--color-grey-light-1);
    text-decoration: none;
    text-transform: uppercase;
    display: block;
    padding: 1.5rem 3rem;
    position: relative;
    z-index: 10;

    display: flex;
    align-items: center;

    // 86.
    @media only screen and (max-width: $bp-medium) {
      justify-content: center;
      padding: 2rem;
    }
  }
  //   &__link:hover {
  //     color: orangered;
  //   }

  &__icon {
    width: 1.75rem;
    height: 1.75rem;
    margin-right: 2rem;
    fill: currentColor;
  }
}

////////////////////////////////////////
// LEGAL TEXT

.legal {
  font-size: 1.2rem;
  text-align: center;
  color: --color-grey-dark-4;
  padding: 2.5rem;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    display: none;
  }
}

////////////////////////////////////////
// GALLERY
.gallery {
  display: flex;

  &__photo {
    width: 100%;
    // PRO-tip, display as block to remove whitespace
    // that would appear if using display: inline
    display: block;
  }
}

////////////////////////////////////////
// HOTEL OVERVIEW
.overview {
  display: flex;
  align-items: center;
  border-bottom: var(--line);

  &__heading {
    font-size: 2.25rem;
    font-weight: 300;
    text-transform: uppercase;
    letter-spacing: 1px;
    padding: 1.5rem 3rem;
  }

  &__stars {
    margin-right: auto;
    // remove the whitespace caused by svg as they
    // behave like text and leave a small whitespace at the bottom
    display: flex;
  }

  &__icon-star,
  &__icon-location {
    width: 1.75rem;
    height: 1.75rem;
    fill: var(--color-primary);
  }

  &__location {
    font-size: 1.2rem;
    display: flex;
    vertical-align: center;
  }

  &__icon-location {
    margin-right: 0.5rem;
  }

  &__rating {
    background-color: var(--color-primary);
    color: #fff;
    margin-left: 3rem;
    padding: 0 2.25rem;
    align-self: stretch;

    flex-direction: column;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__rating-average {
    font-size: 2.25rem;
    font-weight: 300;
    margin-bottom: -3px;
  }

  &__rating-count {
    font-size: 0.8rem;
    text-transform: uppercase;
  }
}

////////////////////////////////////////
// BUTTON INLINE
.btn-inline {
  border: none;
  color: var(--color-primary);
  font-size: inherit;
  border-bottom: 1px solid currentColor;
  padding-bottom: 2px;
  display: inline-block;
  background-color: transparent;
  cursor: pointer;
  transition: all 0.2s;

  // 84.
  & span {
    margin-left: 3px;
    transition: margin-left 0.2s;
  }

  &:hover {
    color: var(--color-grey-dark-1);

    span {
      margin-left: 8px;
    }
  }

  // Animate
  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

@keyframes pulsate {
  0% {
    transform: scale(1);
    box-shadow: none;
  }

  50% {
    transform: scale(1.05);
    box-shadow: 0 1rem 4rem rgba(0, 0, 0, 0.25);
  }

  100% {
    transform: scale(1);
    box-shadow: none;
  }
}

////////////////////////////////////////
// PARAGRAPH
.paragraph:not(:last-of-type) {
  margin-bottom: 2rem;
}

////////////////////////////////////////
// LIST
.list {
  list-style: none;
  margin: 3rem 0;
  padding: 3rem 0;
  border-top: var(--line);
  border-bottom: var(--line);

  display: flex;
  flex-wrap: wrap;

  &__item {
    flex: 0 0 50%;
    margin-bottom: 0.7rem;
  }

  // NOTE 83. TIP TO CHANGE THE COLOR OF THE SVG ICON
  &__item::before {
    content: "";
    display: inline-block;
    height: 1rem;
    width: 1rem;
    margin-right: 0.7rem;
    // older browsers
    // background-image: url(../img/chevron-thin-right.svg);
    // background-size: cover;

    // Newer Browsers - masks
    background-color: var(--color-primary);
    -webkit-mask-image: url(../img/chevron-thin-right.svg);
    -webkit-mask-size: cover;
    mask-image: url(../img/chevron-thin-right.svg);
    mask-size: cover;
  }
}

////////////////////////////////////////
// 83. RECOMMEND
.recommend {
  font-size: 1.3rem;
  color: var(--color-grey-dark-3);

  display: flex;
  align-items: center;

  &__count {
    margin-right: auto;
  }

  // 86. Keep photos side by side
  &__friends {
    display: flex;
  }

  &__photo {
    // prevent border from shrinking size of photo with content-box
    box-sizing: content-box;
    height: 4rem;
    width: 4rem;
    border-radius: 50%;
    border: 3px solid #fff;

    &:not(:last-child) {
      margin-right: -2rem;
    }
  }
}

////////////////////////////////////////
// 84. REVIEWS
.review {
  background-color: #fff;
  box-shadow: var(--shadow-light);
  padding: 3rem;
  margin-bottom: 3.5rem;
  position: relative;
  overflow: hidden;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 2rem;
    margin-bottom: 3rem;
  }

  &__text {
    margin-bottom: 2rem;

    // z-index only works if position is set
    z-index: 10;
    position: relative;
  }

  &__user {
    display: flex;
    align-items: center;
  }

  &__photo {
    height: 4.5rem;
    width: 4.5rem;
    border-radius: 50%;
    margin-right: 1.5rem;
  }

  &__user-box {
    // gives margin between user-name, user-date from user-rating
    margin-right: auto;
  }

  &__user-name {
    font-size: 1.1rem;
    font-weight: 600;
    text-transform: uppercase;
    margin-bottom: 0.4rem;
  }

  &__user-date {
    font-size: 1rem;
    color: var(--color-grey-dark-3);
  }

  &__rating {
    color: var(--color-primary);
    font-size: 2.2rem;
    font-weight: 300;
  }

  &::before {
    // entity code for quotation marks, from CSStricks.com
    content: "\201C";
    position: absolute;
    top: -2.75rem;
    left: -1rem;
    line-height: 1;
    font-size: 20rem;
    color: var(--color-grey-light-2);
    font-family: sans-serif;
    z-index: 1;
  }
}

////////////////////////////////////////
// 85. CALL TO ACTION
.cta {
  padding: 3.5rem 0;
  text-align: center;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 2rem 0;
  }

  &__book-now {
    font-size: 2rem;
    font-weight: 300;
    text-transform: uppercase;
    margin-bottom: 2.5rem;
  }
}

////////////////////////////////////////
// 85. CALL TO ACTION
.btn {
  font-size: 1.5rem;
  font-weight: 300;
  text-transform: uppercase;
  border-radius: 100px;
  border: none;
  background-image: linear-gradient(
    to right,
    var(--color-primary-light),
    var(--color-primary-dark)
  );
  color: #fff;
  position: relative;
  //hide the text that is outside the book now button
  overflow: hidden;
  cursor: pointer;

  & > * {
    display: inline-block;
    height: 100%;
    width: 100%;
    transition: all 0.2s;
  }

  &__visible {
    //inline block to use padding
    padding: 2rem 7.5rem;
  }

  &__invisible {
    position: absolute;
    padding: 2rem 0;
    left: 0;
    top: -100%;
  }

  &:hover {
    background-image: linear-gradient(
      to left,
      var(--color-primary-light),
      var(--color-primary-dark)
    );
  }

  &:hover &__visible {
    // we dont use top property because
    // we did not set position to absolute on it
    transform: translateY(100%);
  }

  &:hover &__invisible {
    top: 0;
  }

  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

```

## 87. Writing Media Queries - Part 2

components.scss

```
////////////////////////////////////////
// LOGO
.logo {
  height: 3.25rem;
  margin-left: 2rem;
}
////////////////////////////////////////
// SEARCH
.search {
  // 76.
  flex: 0 0 40%;

  // align magnifying glass in the search bar
  // nested flex-box , item given flex container property
  display: flex;
  align-items: center;
  justify-content: center;

  // 86.
  @media only screen and (max-width: $bp-smallest) {
    order: 1;
    flex: 0 0 100%;
    background-color: var(--color-grey-light-2);
  }

  &__input {
    font-family: inherit;
    font-size: inherit;
    color: inherit;
    background-color: var(--color-grey-light-2);
    border: none;
    padding: 0.7rem 2rem;
    border-radius: 100px;
    width: 90%;
    transition: all 0.2s;
    // trick to move button on top of the input bar
    margin-right: -3.25rem;

    &:focus {
      outline: none;
      width: 100%;
      background-color: var(--color-grey-light-3);
    }

    // change placeholder text
    &::-webkit-input-placeholder {
      font-weight: 100;
      color: var(--color-grey-light-4);
    }
  }

  // adjacent selector (for siblings)
  &__input:focus + &__button {
    background-color: var(--color-grey-light-3);
  }

  &__button {
    border: none;
    background-color: var(--color-grey-light-2);

    &:focus {
      outline: none;
    }

    &:active {
      transform: translateY(2px);
    }
  }

  &__icon {
    height: 2rem;
    width: 2rem;
    // change svg color
    fill: var(--color-grey-dark-3);
  }
}
////////////////////////////////////////
// 78. USER NAVIGATION
.user-nav {
  align-self: stretch;
  display: flex;
  align-items: center;

  // select direct children of .user-nav
  & > * {
    padding: 0 2rem;
    cursor: pointer;
    height: 100%;
    display: flex;
    align-items: center;
  }

  & > *:hover {
    background-color: var(--color-grey-light-2);
  }

  &__icon-box {
    position: relative;
  }

  &__icon {
    height: 2.25rem;
    width: 2.25rem;
    fill: var(--color-grey-dark-2);
  }

  &__notification {
    font-size: 0.8rem;
    height: 1.75rem;
    width: 1.75rem;
    border-radius: 50%;
    background-color: var(--color-primary);
    color: #fff;

    // Placement
    position: absolute;
    top: 1.5rem;
    right: 1.1rem;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__user-photo {
    height: 3.75rem;
    border-radius: 50%;
    margin-right: 1rem;
  }
}

////////////////////////////////////////
// SIDE NAVIGATION
.side-nav {
  font-size: 1.4rem;
  list-style: none;
  margin-top: 3.5rem;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    display: flex;
    margin: 0;
  }

  &__item {
    position: relative;

    &:not(:last-child) {
      margin-bottom: 0.5rem;

      // 86.
      @media only screen and (max-width: $bp-medium) {
        margin: none;
      }
    }
    // 86.
    @media only screen and (max-width: $bp-medium) {
      flex: 1;
    }
  }

  &__item::before {
    content: "";
    position: absolute;
    top: 0;
    height: 100%;
    width: 3px;
    background-color: var(--color-primary);
    transform: scaleY(0);

    //transform-origin: bottom;
    // add delay to transfor width
    transition: transform 0.2s, width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s,
      background-color 0.1s;
  }

  &__item:hover::before,
  &__item--active::before {
    transform: scaleY(1);
    width: 100%;
  }

  // make button brighter color to show active state
  &__item:active::before {
    background-color: var(--color-primary-light);
  }

  &__link:link,
  &__link:visited {
    color: var(--color-grey-light-1);
    text-decoration: none;
    text-transform: uppercase;
    display: block;
    padding: 1.5rem 3rem;
    position: relative;
    z-index: 10;

    display: flex;
    align-items: center;

    // 86.
    @media only screen and (max-width: $bp-medium) {
      justify-content: center;
      padding: 2rem;
    }

    // 87.
    @media only screen and (max-width: $bp-small) {
      flex-direction: column;
      padding: 1.5rem 0.5rem;
    }
  }
  //   &__link:hover {
  //     color: orangered;
  //   }

  &__icon {
    width: 1.75rem;
    height: 1.75rem;
    margin-right: 2rem;
    fill: currentColor;

    // 87.
    @media only screen and (max-width: $bp-small) {
      margin-right: 0;
      margin-bottom: 0.7rem;
      width: 1.5rem;
      height: 1.5rem;
    }
  }
}

////////////////////////////////////////
// LEGAL TEXT

.legal {
  font-size: 1.2rem;
  text-align: center;
  color: --color-grey-dark-4;
  padding: 2.5rem;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    display: none;
  }
}

////////////////////////////////////////
// GALLERY
.gallery {
  display: flex;

  &__photo {
    width: 100%;
    // PRO-tip, display as block to remove whitespace
    // that would appear if using display: inline
    display: block;
  }
}

////////////////////////////////////////
// HOTEL OVERVIEW
.overview {
  display: flex;
  align-items: center;
  border-bottom: var(--line);

  &__heading {
    font-size: 2.25rem;
    font-weight: 300;
    text-transform: uppercase;
    letter-spacing: 1px;
    padding: 1.5rem 3rem;

    // 87.
    @media only screen and (max-width: $bp-small) {
      font-size: 1.8rem;
      padding: 1.25rem 2rem;
    }
  }

  &__stars {
    margin-right: auto;
    // remove the whitespace caused by svg as they
    // behave like text and leave a small whitespace at the bottom
    display: flex;
  }

  &__icon-star,
  &__icon-location {
    width: 1.75rem;
    height: 1.75rem;
    fill: var(--color-primary);
  }

  &__location {
    font-size: 1.2rem;
    display: flex;
    vertical-align: center;
  }

  &__icon-location {
    margin-right: 0.5rem;
  }

  &__rating {
    background-color: var(--color-primary);
    color: #fff;
    margin-left: 3rem;
    padding: 0 2.25rem;
    align-self: stretch;

    flex-direction: column;
    display: flex;
    align-items: center;
    justify-content: center;

    // 87.
    @media only screen and (max-width: $bp-small) {
      padding: 0 1.5rem;
    }
  }

  &__rating-average {
    font-size: 2.25rem;
    font-weight: 300;
    margin-bottom: -3px;

    // 87.
    @media only screen and (max-width: $bp-small) {
      font-size: 1.8rem;
    }
  }

  &__rating-count {
    font-size: 0.8rem;
    text-transform: uppercase;

    // 87.
    @media only screen and (max-width: $bp-small) {
      padding: 0 0.5rem;
    }
  }
}

////////////////////////////////////////
// BUTTON INLINE
.btn-inline {
  border: none;
  color: var(--color-primary);
  font-size: inherit;
  border-bottom: 1px solid currentColor;
  padding-bottom: 2px;
  display: inline-block;
  background-color: transparent;
  cursor: pointer;
  transition: all 0.2s;

  // 84.
  & span {
    margin-left: 3px;
    transition: margin-left 0.2s;
  }

  &:hover {
    color: var(--color-grey-dark-1);

    span {
      margin-left: 8px;
    }
  }

  // Animate
  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

@keyframes pulsate {
  0% {
    transform: scale(1);
    box-shadow: none;
  }

  50% {
    transform: scale(1.05);
    box-shadow: 0 1rem 4rem rgba(0, 0, 0, 0.25);
  }

  100% {
    transform: scale(1);
    box-shadow: none;
  }
}

////////////////////////////////////////
// PARAGRAPH
.paragraph:not(:last-of-type) {
  margin-bottom: 2rem;
}

////////////////////////////////////////
// LIST
.list {
  list-style: none;
  margin: 3rem 0;
  padding: 3rem 0;
  border-top: var(--line);
  border-bottom: var(--line);

  display: flex;
  flex-wrap: wrap;

  &__item {
    flex: 0 0 50%;
    margin-bottom: 0.7rem;
  }

  // NOTE 83. TIP TO CHANGE THE COLOR OF THE SVG ICON
  &__item::before {
    content: "";
    display: inline-block;
    height: 1rem;
    width: 1rem;
    margin-right: 0.7rem;
    // older browsers
    // background-image: url(../img/chevron-thin-right.svg);
    // background-size: cover;

    // Newer Browsers - masks
    background-color: var(--color-primary);
    -webkit-mask-image: url(../img/chevron-thin-right.svg);
    -webkit-mask-size: cover;
    mask-image: url(../img/chevron-thin-right.svg);
    mask-size: cover;
  }
}

////////////////////////////////////////
// 83. RECOMMEND
.recommend {
  font-size: 1.3rem;
  color: var(--color-grey-dark-3);

  display: flex;
  align-items: center;

  &__count {
    margin-right: auto;
  }

  // 86. Keep photos side by side
  &__friends {
    display: flex;
  }

  &__photo {
    // prevent border from shrinking size of photo with content-box
    box-sizing: content-box;
    height: 4rem;
    width: 4rem;
    border-radius: 50%;
    border: 3px solid #fff;

    &:not(:last-child) {
      margin-right: -2rem;
    }
  }
}

////////////////////////////////////////
// 84. REVIEWS
.review {
  background-color: #fff;
  box-shadow: var(--shadow-light);
  padding: 3rem;
  margin-bottom: 3.5rem;
  position: relative;
  overflow: hidden;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 2rem;
    margin-bottom: 3rem;
  }

  &__text {
    margin-bottom: 2rem;

    // z-index only works if position is set
    z-index: 10;
    position: relative;
  }

  &__user {
    display: flex;
    align-items: center;
  }

  &__photo {
    height: 4.5rem;
    width: 4.5rem;
    border-radius: 50%;
    margin-right: 1.5rem;
  }

  &__user-box {
    // gives margin between user-name, user-date from user-rating
    margin-right: auto;
  }

  &__user-name {
    font-size: 1.1rem;
    font-weight: 600;
    text-transform: uppercase;
    margin-bottom: 0.4rem;
  }

  &__user-date {
    font-size: 1rem;
    color: var(--color-grey-dark-3);
  }

  &__rating {
    color: var(--color-primary);
    font-size: 2.2rem;
    font-weight: 300;
  }

  &::before {
    // entity code for quotation marks, from CSStricks.com
    content: "\201C";
    position: absolute;
    top: -2.75rem;
    left: -1rem;
    line-height: 1;
    font-size: 20rem;
    color: var(--color-grey-light-2);
    font-family: sans-serif;
    z-index: 1;
  }
}

////////////////////////////////////////
// 85. CALL TO ACTION
.cta {
  padding: 3.5rem 0;
  text-align: center;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 2rem 0;
  }

  &__book-now {
    font-size: 2rem;
    font-weight: 300;
    text-transform: uppercase;
    margin-bottom: 2.5rem;
  }
}

////////////////////////////////////////
// 85. CALL TO ACTION
.btn {
  font-size: 1.5rem;
  font-weight: 300;
  text-transform: uppercase;
  border-radius: 100px;
  border: none;
  background-image: linear-gradient(
    to right,
    var(--color-primary-light),
    var(--color-primary-dark)
  );
  color: #fff;
  position: relative;
  //hide the text that is outside the book now button
  overflow: hidden;
  cursor: pointer;

  & > * {
    display: inline-block;
    height: 100%;
    width: 100%;
    transition: all 0.2s;
  }

  &__visible {
    //inline block to use padding
    padding: 2rem 7.5rem;
  }

  &__invisible {
    position: absolute;
    padding: 2rem 0;
    left: 0;
    top: -100%;
  }

  &:hover {
    background-image: linear-gradient(
      to left,
      var(--color-primary-light),
      var(--color-primary-dark)
    );
  }

  &:hover &__visible {
    // we dont use top property because
    // we did not set position to absolute on it
    transform: translateY(100%);
  }

  &:hover &__invisible {
    top: 0;
  }

  &:focus {
    outline: none;
    animation: pulsate 1s infinite;
  }
}

```

layout.scss

```
.container {
  // 86.
  @media only screen and (max-width: $bp-largest) {
    margin: 0;
    max-width: 100%;
    width: 100%;
    margin: 0;
  }

  max-width: 120rem;
  margin: 8rem auto;
  background-color: var(--color-grey-light-2);
  box-shadow: var(--shadow-dark);
  min-height: 50rem;
}

.header {
  font-size: 1.4rem;
  height: 7rem;
  background-color: #fff;
  border-bottom: var(--line);

  display: flex;
  // 76. align along main axis
  justify-content: space-between;
  // align along cross axis
  align-items: center;
  // 86.
  @media only screen and (max-width: $bp-smallest) {
    flex-wrap: wrap;
    height: 12rem;
    // space between rows
    align-content: space-around;
  }
}

.content {
  display: flex;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    flex-direction: column;
  }
}

.sidebar {
  background-color: var(--color-grey-dark-1);

  // grow shrink basis
  flex: 0 0 18%;

  // placing legal text at bottom of page
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.hotel-view {
  //background-color: #fff;

  flex: 1;
}

.detail {
  font-size: 1.4rem;
  display: flex;
  padding: 4.5rem;
  background-color: var(--color-grey-light-1);
  border-bottom: var(--line);

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 3rem;
  }

  // 87.
  @media only screen and (max-width: $bp-small) {
    flex-direction: column;
  }
}

.description {
  // NOTE font-size is inherited from parent element
  background-color: #fff;
  box-shadow: var(--shadow-light);
  padding: 3rem;
  flex: 0 0 60%;
  margin-right: 4.5rem;

  // 86.
  @media only screen and (max-width: $bp-medium) {
    padding: 2rem;
    margin-right: 3rem;
  }

  // 87.
  @media only screen and (max-width: $bp-small) {
    margin-right: 0;
    margin-bottom: 3rem;
  }
}

.user-reviews {
  flex: 1;

  // 84.
  display: flex;
  flex-direction: column;
  align-items: center;
}

```
