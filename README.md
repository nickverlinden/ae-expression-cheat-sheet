# Adobe After Effects Expression Cheat Sheet

## Table Of Contents
 - [Globals](#globals)
   - [Contextual](#contextual)
     - [Objects](#objects)
     - [Project](#project)
   - [Static](#static)
     - [Functions](#functions)
      - [Time Conversion](#time-conversion)
      - [Locating Project Elements](#locating-project-elements)


## Globals

### Contextual Variables

#### Objects
Object | Description | Example
------ | ----------- | -------
`thisComp` | Current composition | ```thisComp;```
`thisLayer` | Current layer | ```thisLayer.transform.scale[1];```
`thisProperty` | Current property the expression is applied upon. | ```thisProperty[1];```
`time` | Current timecode at cursor position in seconds. | ```"Seconds: " + time;```
`value` | Current value associated to the current property. | ```value + "_TEST";```

### Project
Object | Description | Example
------ | ----------- | -------
`colorDepth` | Project color depth in bits per pixel. | ```colorDepth;```

### Composition Object Properties & Functions
Function | Description 
-------- | ----------- 
`layer(index \|\| number)` | Returns a Layer, Light or Camera object.
`layer(layer, relIndex)` | Returns the object with a relative index to the given layer.


### Functions

#### Time Conversion

Function | Description | Example
-------- | ----------- | -------
`framesToTime(frames, fps)` | Convert frames to timecode in seconds. | ```framesToTime(50, 1.0 / thisComp.frameDuration);```
`timeToCurrentFormat(t, fps, isDuration)` | Converts timecode to the current Project Settings display format. | |
`timeToFeetAndFrames(t, fps, framesPerFoot, isDuration)` | Converts timecode to feet and frames format. | |
`timeToFrames(t, fps, isDuration)` | Converts timecode to frames. | |
`timeToNTSCTimecode(t, ntscDropFrame, isDuration)` | Converts timecode to NTSC timecode with or without drop frame. | |
`timeToTimecode(t, timecodeBase, isDuration)` | Converts timecode to other timecode using the given timebase. | |

#### Locating Project Elements

Function | Description | Example
-------- | ----------- | -------
`comp(name)` | Find the open composition with the given name. | ```comp("Comp 1");```
`footage(name)` | Find the project footage with the given name. | ```footage("RedHarring.png");```

### Tips & Tricks

#### Set Size And Position Of Shape To Text

**You have:**

* Text Layer
* Shape Layer

**You want to:**

* Set the shape to the size and position of the text.

**Solution:**

Let's say you have a shape layer with a rectangle shape.

* Add following expression to the rectangle path's size property

```javascript
var textLayer = thisComp.layer("Text Layer 1");
var textRect = textLayer.sourceRectAtTime(time - textLayer.inPoint, true);

// set size of rectangle path to text rectangle's width and height
[textRect.width, textRect.height];
```
This will set the size of the rectangle to the size of the text. When there
are multiple lines, it takes the full size of all lines.

* Add following expression to the rectangle path's position property

```javascript
var rectPath = content("Rectangle 1").content("Rectangle Path 1");
var x = rectPath.size[0];
var y = rectPath.size[1];

// set position of rectangle path to text rectangle's width and height
[x/2, -(y/2)];
```
This sets the bottom left position of the rectangle's path to top left of the layer. Text Layers
always have their anchor points on the bottom left of the first line of text.
This will make the calculation more easy to do.

* Add following expression to the rectangle layer's Transform.Position property

```javascript
var textLayer = thisComp.layer("Text Layer 1");
var textRect = textLayer.sourceRectAtTime(time - textLayer.inPoint, true);
[ textLayer.transform.position[0] + textRect.left,
  textLayer.transform.position[1] + textRect.top + textRect.height ];
```
This sets the position of the rectangle's layer to the position of the
text. The reason for adding the rectangle size, is because the font rendering
can cause the first letter to be a few pixels off the position. Adding the
rectangle coordinates will compensate for that.

**Problems:**
* The text has multiple lines, and you want a rectangle for each line instead of
  one covering all the lines.
* The text has letters that extend the rectangle on the bottom (like the letter q)