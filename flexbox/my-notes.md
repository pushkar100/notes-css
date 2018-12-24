# Flexbox Introduction

Earlier, the layout was based on horizontal (inline) and vertical (block) elements. The box model provided the basis for building layouts.

Flexbox is a **new layout**. It is not just a property but a way of building your UI. It is a shortform for "*Flexible Box Layout Model*". It aims to provide a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word "flex")

*Browser Support*: All major browsers support flexbox (without prefixes). Full support for IE came in **IE 11**. Basically, **95**% of all global browser usage supports flexbox.

*Drawback of flexbox*: If it is not supported then it does not degrade gracefully. It leads to broken UI. Hence, if you need to support users on old browsers, do not use flexbox.

## Syntax

Every flexbox layout needs to contain two things:

- A container 
- One or more items 

We can recognise any element as a flex container by adding **`display: flex;`** property to it. By doing so, any element inside this flex container automatically becomes a flexbox item. And, flex containers can be *nested*!

Flex properties generally override other properties and in case of conflicts of any sort, there could be unexpected behavior. `float`, `clear`, etc **do not** work in a flex layout.

### The Concept of Flexbox Axes

We can think of flexbox container being a plane with two axes:

- **Main** axis
- **Cross** axis

In a *Left-To-Right* text direction layout (`direction: rtl`, usually default and for english), the flexbox main axis is **horizontal** by default (and cross axis is vertical).

```
(start)--------------------(end)--> (main)
|
|
|
|
(end)
|
\/
cross
```

In a *Right-To-Left* text direction layout (`direction: rtl`, example: Arabic), the main axis is still **horizontal** by default, but the direction of its axis ***is reversed***.

```
(main) <--(end)--------------------(start)
									|
									|
									|
									|
								  (end)
									|
									\/
									cross
```

#### Flex Container Properties

Assuming that text direction `direction: ltr` (left to right). It works in the opposite way for `rtl`.

1. **`flex-direction`**: Sets the main axis of the flow.

   - `row`: *Horizontal* main axis, Flow is from *Left-To-Right*. Origin is *top-left*.
   - `row-reverse`:  *Horizontal* main axis, Flow is from *Right-To-Left*. Origin is *top-right*.
   - `column`: *Vertical* main axis, Flow is from *Top-To-Bottom*. Origin is *top-left*.
   - `column-reverse`: *Vertical* main axis, Flow is from *Bottom-To-Top*. Origin is *top-left*. ***Note***: for origin to be top-right, you need `direction: rtl` to be set.

   ```
   # "row":
   start--------------------end--> [MAIN AXIS]
   
   # "row-reverse":
   <--end--------------------start [MAIN AXIS]
   
   # "column":
   start
   |
   |
   |
   |
   end
   |
   \/
   [MAIN AXIS]
   
   # "column-reverse":
   /\
   |
   end
   |
   |
   |
   |
   start
   [MAIN AXIS]
   ```

2. **`flex-wrap`**: Determins if and how the flex items must be wrapped inside the container.

   - `nowrap`: The items are not wrapped onto the next line. All the items are on the same line. However, there is no overflow. Instead, the items are squished tightly together according to their proportions if they exceed the available space on the line.
   - `wrap`: Wraps the elements if the space available on one line is exceeded.
   - `wrap-reverse`: Wraps but in reverse order. If wrapping was from top to bottom, then wrap-reverse will be from *bottom-to-top*.
   - [`flex-wrap` demo](https://css-tricks.com/almanac/properties/f/flex-wrap/)

3. **`flex-flow`**: It is a ***shorthand*** for direction and wrap. 

   - Syntax: `flex-flow: flex-direction flex-wrap;`

   - Default value: `flex-flow: row nowrap;`

4. **`justify-content`**: It *aligns items on the main axis*. As an example, if `flex-direction: row` then the items are aligned horizontally (assuming `ltr`).

   - `flex-start`: Items are aligned to start of the main axis.
   - `flex-end`: Items are aligned to end of the main axis.
   - `center`: Items are aligned to the center of the main axis.
   - `space-between`: The extreme elements touch start and end of main axis and elements in between are evenly spaced out. Similar to `text-align` but for block elements.
   - `space-around`: The extreme elements do not touch start and end of the main axis. All the elements are evenly spaced out with half the amount of spacing left on each extreme side as is in between.
   - `space-evenly`: The extreme elements do not touch start and end of the main axis. All the elements are evenly spaced out with the same, equal the amount of spacing left on each extreme side as well.
   - `stretch`: The items are stretched out on the main axis. Sometimes `height` property could interfere with it and in that case, `height: auto` will allow stretch to work.
   - `normal`: No spcecific alignment.
   
![`justify-content` visualization](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg)

5. **`align-items`**: It *aligns items on the cross axis*.

   - `flex-start`
   - `flex-end`
   - `center`
   - `stretch`
   - `baseline`

6. **`align-content`**: It is used to *manage the space between multiple lines* when flex items are *wrapped* inside a container. It has no effect if `flex-wrap: nowrap` is set (or on any single-line containers).

   - `flex-start`
   - `flex-end`
   - `center`
   - `space-around`
   - `space-between`

#### Flex Item Properties

1. **`flex-grow`**: Defines a proprtion by which an item ***grows*** inside the container. It accepts positive integer or floating point values.
   - `1`: *Default value*, equal growth. The item grows just as much as the container's growth.
   - `2`: The item grows twice as much as the container's growth. 
   - `1.5` *... and so on.*
2. **`flex-shrink`**: Defines a proportion by which an item ***shrinks*** inside the container. It too accepts positive integer or floating point values.
   - `1`: *Default value*, equal shrink. The item shrinks just as much as the container's shrink.
   - `2`: The item shrinks twice as much as the container's shrink.
   - `1.5` *... and so on.*
3. **`flex-basis`**: This defines the default size of an element before the remaining space is distributed. Similar to `width` or `height` and it takes precedence over them. The difference is that it does not overflow the container in case the value is high, it gets squished (is shrunk) accordingly.
   - `auto`: *Default value*.
   - `px`, `%`, `em`, `pt`, etc values can be set.
4. **`flex`**: It is a ***shorthand*** for grow, shrink and basis.
   - Syntax: `flex: flex-grow flex-shrink flex-basis`
   - Default value: `flex: 1 1 auto`
5. **`align-self`**: It is similar to `align-items` property on the container. That is, it aligns the items on the cross axis. The difference is, `align-self` is applied to one item or a subset of items and overrides `align-items` for those items.
   - `flex-start`
   - `flex-end`
   - `center`
   - `baseline`
   - `stretch`
6. **`order`**: Orders a particular element visually with respect to other items inside the container. You can think of it as being vaguely similar to `z-index`. It accepts any integer value, including negative ones. It places smaller valued items at the start and higher valued items at the end. (It sorts items in ascending order from start position)
   - `0`: *Default value*. 
   - Example of a row (horizontal) container items `[]`: 
     - `[order -1][order 0] [order 0] [order 1] [order 3]`

### Applications of Flexbox

Do not use it to build an entire layout. Similar to `position`, a property that you will not use to build entire layouts but only certain components, use flexbox for intricate layouts only. The reason is that flexbox can take elements out of the normal flow as defined in the source document (HTML) and disrupts the original layout. Some examples for the right use of flexboxes are:

1. Flexible navigation
2. Form control (Aligns fields and inputs nicely, in a flexible and fluid manner)
3. Vertical centering of elements (Flexbox makes it easy)
4. Multiple column layouts (Especially when fluid and fixed width items are present in the same container)

## More

1. Practice flexbox: http://flexboxfroggy.com
2. A thorough guide: https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-basics
3. W3Schools article: https://www.w3schools.com/css/css3_flexbox.asp
