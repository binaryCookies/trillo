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
