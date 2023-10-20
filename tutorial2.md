```template
let minutes = -0
let hours = 1
basic.forever(function () {
    basic.showNumber(hours)
    basic.pause(60000)
    minutes += 1
    changetime()
})

function changetime () {
    if (minutes == 60) {
        hours += 1
        minutes = 0
    }
    if (hours == 13) {
        hours = 1
    }
}
```
# Halo Light Clock Part 2
## Introduction
This tutorial is a continuation of the previous tutorial which can be found [here](https://makecode.microbit.org/#tutorial:github:madmatt22790/halo_light_tutorial_part_1/tutorial).

If you havent completed this tutorial then do so before starting this one.

In this part of the tutorial we will be adding functionality for the Halo Light to display the minutes variable.
```
Hints will be displayed in here.
```
## Step 1
The first step is to add the NeoPixel extension to our microbit.

``||Neopixel: Testing||``

```blocks
let strip: neopixel.Strip = null

```