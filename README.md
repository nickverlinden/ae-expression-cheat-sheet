# Adobe After Effects Expression Cheat Sheet

## Globals

### Contextual

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

## Static

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

#### Location Project Elements

Function | Description | Example
-------- | ----------- | -------
`comp(name)` | Find the open composition with the given name. | ```comp("Comp 1");```
`footage(name)` | Find the project footage with the given name. | ```footage("RedHarring.png");```

Work In Progress...