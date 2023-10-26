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

First we need to create a new variable called ``||variable: index||`` this will be used in a loop to count how many times the loop has run.

Now drag the ``||variables: set index to 0||`` block and place it underneath the strip clear block. Change the 0 to a 1.

Next we are going to drag a ``||loops: while||`` loop in and place it underneath our strip clear block.
```blocks
function lights () {
    strip.clear()
    let index = 1
    // @highlight
    while (false) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 5
Next we are need to tell the while loop when to stop running. This is determined by whatever logic we place into the diamond shaped space on the block. Currently it is set to false.

Within our Logic tab drag a diamond ``||logic: comparision||`` block into the space on the block.

Drag our ``||variables: index||`` variable into the first 0 space on the comparision block.
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= 0) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 6
Now we need to do some maths. We want our LED's to light up in batches of two but only if the minutes is divisible by 5.

First we need to check how many should be lit up when we divide our minutes by 5.

The first problem is that if we just do a simple division numbers which aren't divisible by 5 will end up being decimals which will not work for telling the strip which LED's to light up.

So for this reason we are going to want to always round down our number after it has been divided so that it is always a whole number rather than a fraction.

In coding we use a special block called ``||math: floor||`` which will take whatever number is put in and round it down to the nearest whole number. Drag this into the second 0 space in the comparison block.

You can get this block by dragging the ``||math: round||`` block in and changing it to floor with the drop down menu.
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(0)) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```
## Step 7
The next problem we need to solve is that if we simply divide our minutes by 5 our number is going to be too small. 

For example if the minutes is at 60 and we divide it by 5 we will get 12 but we want all 24 lights be lit up. So to solve this we are going to multiple the end number by 2

Our equation is going to look like this minutes / 5 * 2. Which is then rounded down.

Using our Maths blocks we can drag in the appropriate equations so that our final equation looks like it does in the hints of this step. 
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {}
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 8
Now we can start lighting up the Halo Light. 

We do this by dragging a ``||neopixel: strip set pixel color at 0 to red||`` into our ``||loops: while||`` loop block.

The way this block works is that it sets the colour of of an LED to an indicated colour. 

The LED's are assigned a number with 0 being the top LED and continuing around in a clockwise fashion until 24.

This brings us to the reason that we set the inital index to 1 because we are going to loop through and change the colour of the LED which matches the index number and the LED whose number is 1 less than the current index value.

Let start by setting the colour of the first LED which will be referenced by the current index value minus 1.

Drag a maths block into the 0 of the set pixel colour block, change the symbol to minus then drag the index varaible to the left of the minus and change the 0 to a 1.
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        strip.setPixelColor(index - 1, neopixel.colors(NeoPixelColors.Red))
    }
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```