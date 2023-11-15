```template
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
basic.forever(function () {
    basic.showNumber(hours)
    basic.pause(60000)
    minutes += 1
    changetime()
    lights()
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

function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        strip.setPixelColor(index - 1, neopixel.rgb(255,255,255))
        strip.setPixelColor(index, neopixel.rgb(255,255,255))
        strip.setBrightness(10)
        index += 2
    }
    strip.show()
}
```

```package
neopixel=github:microsoft/pxt-neopixel#v0.7.5
```
# Halo Light Clock Part 2
## Introduction
This tutorial is a continuation of the previous two tutorial which can be found [here](https://makecode.microbit.org/#tutorial:github:madmatt22790/halo_light_tutorial_part_1/tutorial) and [here](https://makecode.microbit.org/#tutorial:github:madmatt22790/halo_light_tutorial_part_1/tutorial2).

If you havent completed the two tutorials yet then do so before starting this one.

In this part of the tutorial we will be adding a function to set the time manually using the buttons on the micro:setBrightness

## Step 1
First we need to create a variable that stores a Boolean.

A Boolean is either true or false and we are going to use ours to store whether we are setting the time (true) or not setting the time (false).

Under the ``||variables: variables||`` heading choose "Make a Variable" and name this variable "reset".

Drag the ``||variables: set reset to 0||`` block into the starting code block.

```blocks
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
// @highlight
let reset = 0
```

## Step 2
Next we need to define what are starting state for our reset variable is going to be.

Under the ``||variables: variables||`` section there are two diamond blocks one saying true the other false. Despite these blocks being a diamond shape and our variable being a circular shape the diamond true block can be dragged into a variable.

Do this to set our reset variable to start as false.

```blocks
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
// @highlight
let reset = false
```

## Step 3
Now we need a way to tell the microbit to enter into the time reset state at the push of a button. 

We are going to do this by pressing the A and B buttons simultaniously. We can set what happens when these button are pressed by going into the ``||input: input||`` section and dragging an "on button A pressed" block into the workspace and using the drop down menu on this block change it to A+B. 
```blocks
input.onButtonPressed(Button.AB, function () {})
```

## Step 4
Within this function we need the code to set the reset variable to true if both buttons are pressed and if the reset variable is currently set to false and then do the opposite.

For this we are going to use an if and else statement. Drag one of those into the block from the ``||logic: logic||`` section.
```blocks
input.onButtonPressed(Button.AB, function () {
    // @highlight
    if (true) {
    } else {
    }
})
```

## Step 5
Now we are going to check if the reset is true. Do this by grabbing a comparison block and placing it in the section of the if and else block that currently says true.

Next drag in our ``||variables: reset||`` variable to the first circular spot on the comparision block.

Then finally drag a ``||logic: true||`` block and place it in the second circular spot.
```blocks
input.onButtonPressed(Button.AB, function () {
    // @highlight
    if (reset == true) {
    } else {
    }
})
```

## Step 6
By dragging in a ``||variables: set||`` block from the variables section into the upper portion of the if statement we can change the Boolean stored within reset to false. Do this by changing the appropriate parameters on the ``||variables: set||`` block.

Then by dragging in another one into the bottom section we can make it set the variable to true if reset is not equal to true and set the Boolean to true instead.

We have essentially made a toggle switch that we switch us in and out of reset mode when the A and B buttons are pressed simulatinously.
```blocks
input.onButtonPressed(Button.AB, function () {
    // @highlight
    if (reset == true) {
        reset = false
    } else {
        reset = true
    }
})
```

## Step 7
Now we need to make this toggle switch do something. First we want to make it stop the clock and pause it so that it no longer upticks the minutes variable. 

We will need to modify the code within the ``||basic: forever||`` loop.

Drag an ``||logic: if||`` statement block in and place it at the top of the ``||basic: forever||`` loop.
```blocks
basic.forever(function () {
    // @highlight
    if (true) {}
    basic.showNumber(hours)
    basic.pause(60000)
    minutes += 1
    changetime()
    lights()
})
// @hide
function changetime () {}
// @hide
function lights() {}
```

## Step 8
Inside this if statement drag in the 
- show number block
- pause block
- change minutes block.
```blocks
basic.forever(function () {
    // @highlight
    if (true) {
        basic.showNumber(hours)
        basic.pause(60000)
        minutes += 1
    }
    changetime()
    lights()
})
// @hide
function changetime () {}
// @hide
function lights() {}
```

## Step 9
We now need to define when this if function will run what is inside of it. 
Drag a diamond ``||logic: comparison||`` block into the space on the if statement block. Then drag the reset variable into the first space, make sure the comparison is set to = then finally drag a false diamond block into the other side of the comparison block.

This means that whenever we aren't in reset mode it will continue to calculate the time.
```blocks
basic.forever(function () {
    if (reset == false) {
        basic.showNumber(hours)
        basic.pause(60000)
        minutes += 1
    }
    changetime()
    lights()
})
// @hide
function changetime () {}
// @hide
function lights() {}
```