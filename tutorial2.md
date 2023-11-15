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

We are also going to drag in the ``||function: call lights||`` block and place it underneath the ``||function: changetime||`` block so that the function we are about create is run just after the time is updated.

```blocks
basic.forever(function () {
    basic.showNumber(hours)
    basic.pause(60000)
    minutes += 1
    changetime()
    // @highlight
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

The first problem is that if we just do a simple division, numbers which aren't divisible by 5 will end up being decimals which will not work for telling the strip which LED's to light up.

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

## Step 9
For the colour rather than using the drop down menu to choose a default colour we are going to creat our own custom colours using RGB

RGB stands for the three colours which are used to make other colours. Red, Green, Blue

Depending on the values you choose for each of those colours will depend on the final colour that you get. 

The smallest value that one of the colours can be is 0 with the greatest being 255.

Within the more part of the ``||neopixel: neopixel||`` section is a round block that allows you define the values for red, green, and blue. 

Drag this block in place of the default colour drop down menu. 
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        // @highlight
        strip.setPixelColor(index - 1, neopixel.rgb(255,255,255))
    }
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 9
Lets repeat these last few steps to set the colour of the second LED. This is going to be done by duplicating the block. This can easily be done by right clicking on the set pixel color at choosing duplicate. 

This will create another block which you can place below. the only thing you need to do is remove the -1 so that it is changing the LED in position index.
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        strip.setPixelColor(index - 1, neopixel.rgb(255,255,255))
        // @highlight
        strip.setPixelColor(index, neopixel.rgb(255,255,255))
    }
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 10
Next we are going to change the brightness of the LED's as you may not like them being at full brightness.

To do this drag in the ``||neopixel: Set Brightness||`` block and place it underneath our two set pixel blocks.

Like the RGB values the lowest the brightness can be is 0 (which is off) and 255 (Which is full brightness)

Change the value to a number and find a brightness value which works for you.

```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        strip.setPixelColor(index - 1, neopixel.rgb(255,255,255))
        strip.setPixelColor(index, neopixel.rgb(255,255,255))
        // @highlight
        strip.setBrightness(10)
    }
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Step 11
Finally we meed to increase the index by 2 so it can light up the next set of two LED'second

Drag in from the ``||variables: variables||`` section a Change index by 1 block and change the 1 to a 2.

Along with this we need to tell the Halo Light to show the lights that we have set. We can do this by dragging in a ``||neopixel: strip show||`` block underneath the loop, at the very end of this code section.
```blocks
function lights () {
    strip.clear()
    let index = 1
    while (index <= Math.floor(minutes/5*2)) {
        strip.setPixelColor(index - 1, neopixel.rgb(255,255,255))
        strip.setPixelColor(index, neopixel.rgb(255,255,255))
        strip.setBrightness(10)
        // @highlight
        index += 2
    }
    // @highlight
    strip.show()
}
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
```

## Conclusion
The last thing you need to do after pressing finish here is to switch the coding mode from Blocks to Javascript and change the RGB values to a custom number. 

With that we have now added to our code so that it will now light up the ring to show the minutes of our clock as they elapse.
```blocks
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