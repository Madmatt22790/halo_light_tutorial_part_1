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

```package
neopixel=github:microsoft/pxt-neopixel#v0.7.5
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
The first step is to initiate the halo light and assign it to a variable called strip.

Do this by dragging the provided ``||neopixel: set strip to Nepixel||`` into the on start block

```blocks
let minutes = -0
let hours = 1
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 2
Next we are going to make a custom function which will make the lights, display how many minutes have elapsed.

Under the ``||function:Functions||`` tab choose Make a Function and call this Function ``||function: lights||``

```blocks
function lights() {
}
```

## Step 3
The ``||function: lights||`` function will now appear in your workspace. 

Within this function we are going to add a few blocks the first of which being ``||neopixel: strip clear||``

This will clear the LED strip so that it is ready to light up the new LED's that we would like to illuminate.


Drag those blocks in now. (Some may be in the ``||neopixel: more||`` tab)

```blocks
function lights () {
    // @highlight
    strip.clear()
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 4
Since the ring contains 24 LED's we need to decide what LED's to light up to display the minutes. 

For this tutorial we are going to light up 2 more LED's every 5 minutes so that the circle is gradually filled up. 

You will be able to choose the colours of the LEDS' as we go along.

First we need to check if the current amount of minutes is a multiple of 5 to determine how many LED's need to be lit up. 

We do this with an ``||Logic: if||`` statement block. 

Drag this underneath the ``||neopixel: strip clear||`` block
```blocks
function lights () {
    strip.clear()
    // @highlight
    if (true) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 5
Within the ``||logic: if||`` statement block is a diamond shaped space where we put in our comparison block where we can compare two data types. In this case we are going to compare the remainder of our minutes divided by 5.

If there is no remainder then the number is divisible by 5 otherwise it isn't.

For example if our minutes is at 45 and we divide it by 5 then the remainder will be 0. However if we divide 42 by 5 then we will have a remainder of 2 meaning it isn't divisible by 5.

To add this logic we are going to drag a ``||logic: 0 = 0||`` block and place it into that diamond space. 

```blocks
function lights () {
    strip.clear()
    if (0 == 0) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 6 
Next we need to get the remainder of our minutes divided by 5. 

Thankfully there is a block for this ``||math: remainder of 0/1||``

Drag this in place of the first 0 in our ``||logic: comparison block||``

Then drag the ``||variable: minutes||`` variable into the place of the 0 in the math block and then change the 1 to a 5.
```blocks
function lights () {
    strip.clear()
    if (minutes % 5 == 0) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```