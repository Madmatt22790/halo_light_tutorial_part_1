```template
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
let index = 0
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
# Halo Light Clock Part 3
## Introduction
This tutorial is a continuation of the previous two tutorial which can be found [here](https://makecode.microbit.org/#tutorial:github:madmatt22790/halo_light_tutorial_part_1/tutorial) and [here](https://makecode.microbit.org/#tutorial:github:madmatt22790/halo_light_tutorial_part_1/tutorial2).

If you havent completed the two tutorials yet then do so before starting this one.

In this part of the tutorial we will be adding a function to set the time manually using the buttons on the microBit

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
Next we need to define what the starting state for our reset variable is going to be.

Under the ``||logic: logic||`` section there are two diamond blocks one saying true the other false. Despite these blocks being a diamond shape and our variable being a circular shape the diamond true block can be dragged into a variable.

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

We are going to do this by pressing the A and B buttons simultaneously. We can set what happens when these button are pressed by going into the ``||input: input||`` section and dragging an "on button A pressed" block into the workspace and using the drop down menu on this block change it to A+B. 
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

We have essentially made a toggle switch that will switch us in and out of reset mode when the A and B buttons are pressed simultaneously.
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
Inside this if statement drag in the following blocks
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
We now need to define when the clock is allowed to continue counting the minutes
Drag a diamond ``||logic: comparison||`` block into the space on the if statement block. Then drag the reset variable into the first space, make sure the comparison is set to = then finally drag a false diamond block into the other side of the comparison block.

This means that whenever the reset variable is equal to false (meaning we aren't reseting the time) then it will continue adding time to the appropriate variables. 
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

## Step 10
Now that we have stopped the time we need to create a way for us to switch between setting the minutes or hours.

Once we are in reset mode we are going to set it so that when we press the A button that it will increase the hours variable and when the B button is pressed it will increase the minutes variable.

Drag in an "on button A pressed from the ``||input: input||`` section and place an if statement from the ``||logic: logic||``section. (It isn't necessary to use the if & else statment as just an if statement block will do)

```blocks
input.onButtonPressed(Button.A, function () {
    if (true) {
    }
})
```

## Step 11
We want to make sure that the button presses only do something when we are in reset mode. So we need to add a comparison block into the if statement similar to a couple of steps ago to ensure whatever is put into the if statement block happens when we are in reset mode.

Drag a diamond ``||logic: comparison||`` block into the space on the if statement block. Then drag the reset variable into the first space, make sure the comparison is set to = then finally drag a true diamond block into the other side of the comparison block.

This means that whenever the reset variable is equal to true (meaning we are reseting the time) then it will run the code when the A button is pressed.

```blocks
input.onButtonPressed(Button.A, function () {
    // @highlight
    if (reset == true) {
    }
})
```

## Step 12
Inside this if statement block we are going to place two blocks: once to increase the hours variable, and the other to displace the hours variable value. 

Drag a ``||variables: change hours by 1||`` block inside the if statement. Then drag a ``||basic: show number||`` inside the if statement.

Drag the circular hours variable from the ``||variables: variables||`` tab into the space on the ``||basic: show number||`` block.

```blocks
input.onButtonPressed(Button.A, function () {
    if (reset == true) {
        // @highlight
        hours += 1
        // @highlight
        basic.showNumber(hours)
    }
})
```

## Step 12
Now let's do the same for the minutes variable with an ``||input: on button B pressed||`` block from the input section. Place in our if statement block then add in the blocks to change the minutes variable and display the minutes variable as a number.

```blocks
input.onButtonPressed(Button.B, function () {
    if (reset == true) {
        minutes += 1
        basic.showNumber(minutes)
    }
})
```

## Step 13
Next we want some way to indicate to the user what variable they are currently changing. We can do this by changing the colours of the LED's. So when we are setting the minutes variable the LED's all display one colour and when doing the hours they display another. 

First we need to create a variable that we can flip back and forth between minutes and hours which the lights will then read to display the correct colours.

There isn't any need to define the variable in the on start function but instead we can do this straight into our On Button pressed functions. 

In both the A and B button press functions place a ``||variable: set to||`` block underneath the ``||variable: change by||`` block. Call the new variable "HoursOrMinutes".

In the A Button function drag a ``||text: text||`` block into the HoursOrMinutes variable and set it to "Hours"

In the B Button function drag a ``||text: text||`` block into the HoursOrMinutes variable and set it to "Minutes"

In the A+B Button function drag a ``||text: text||`` block into the HoursOrMinutes variable and set it to "None"
```blocks
input.onButtonPressed(Button.A, function () {
    if (reset == true) {
        hours += 1
        HoursOrMinutes = "Hours"
        basic.showNumber(hours)
    }
})

input.onButtonPressed(Button.B, function () {
    if (reset == true) {
        minutes += 1
        HoursOrMinutes = "Minutes"
        basic.showNumber(minutes)
    }
})

input.onButtonPressed(Button.AB, function () {
    if (reset == true) {
        reset = false
        HoursOrMinutes = "None"
    } else {
        reset = true
    }
})
```

## Step 14
Now moving over to our custom lights function we need to add in a nested if and else statement. 

To start this drag an ``||logic: if/else||`` block and place it underneath the strip clear block. Place inside the else section of this logic block our ``||variables: set index to 1||`` block and our ``||loops: while||`` loop.

```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (true) {

    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(255, 255, 255))
            strip.setPixelColor(index, neopixel.rgb(255, 255, 255))
            strip.setBrightness(10)
            index += 2
    }
    }
    
    strip.show()
}
```

## Step 15
Next we want to define what the logic is for the if statement. Drag a ``||logic: comparison||`` block from the logic section and place it in the diamond space of the if/else statement.
```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (0 == 0) {

    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(255, 255, 255))
            strip.setPixelColor(index, neopixel.rgb(255, 255, 255))
            strip.setBrightness(10)
            index += 2
    }
    }
    
    strip.show()
}
```

## Step 16
Now we need to drag our circular reset ``||variables: variable||`` into the first space then a diamond ``||logic: true||`` block into the second circular space. 

This means that whatever we put into the top secion of the if/else statement will only happen if the reset variable is true. Meaning that we are in reset mode. 
```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (reset == true) {

    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(255, 255, 255))
            strip.setPixelColor(index, neopixel.rgb(255, 255, 255))
            strip.setBrightness(10)
            index += 2
    }
    }
    
    strip.show()
}
```

## Step 17
Next drag another ``||logic: if/else||`` statement block inside the top section of the first if/else block.

Then press the little plus symbol at the bottom of this block so our new if/else block turns into an if/else if/else block.

```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (reset == true) {
        // @highlight
        if (0 == 0) {
        } else if (0 == 0) {
        } else {
        }
    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(255, 255, 255))
            strip.setPixelColor(index, neopixel.rgb(255, 255, 255))
            strip.setBrightness(10)
            index += 2
    }
    }
    
    strip.show()
}
```

## Step 18 
This logic is going to allow us to give rules for three different scenarios with our "HoursOrMinutes" variable. 

First if the HoursOrMinutes variable is equal to hours display one colour.

Second if the HoursOrMinutes variable is equal to minutes display a different colour.

Lastly if the HoursOrMinutes variable is equal to anything else display a third colour. 

By now you should be familiar with the logic of adding a ``||logic: comparison||`` block and draggin in the circular ``||logic: HoursOrMinutes||`` variable block into the left side of the comparison and on the other side comparing it to the text "Hours" or "Minutes".
```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (reset == true) {
        if (HoursOrMinutes == "Hours") {
        } else if (HoursOrMinutes == "Minutes") {
        } else {
        }
    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(255, 255, 255))
            strip.setPixelColor(index, neopixel.rgb(255, 255, 255))
            strip.setBrightness(10)
            index += 2
        }
    }
    strip.show()
}
```

## Step 19
Finally lets add in three blocks, one ot each section of the if/else if/else statement block to define the colours when in each mode. 

Drag a ``||neopixel: strip show Color||`` block in and choose a colour.

Do this for the other two sections.

```blocks
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
function lights () {
    strip.clear()
    if (reset == true) {
        if (HoursOrMinutes == "Hours") {
            strip.showColor(neopixel.colors(NeoPixelColors.Green))
        } else if (HoursOrMinutes == "Minutes") {
            strip.showColor(neopixel.colors(NeoPixelColors.Orange))
        } else {
            strip.showColor(neopixel.colors(NeoPixelColors.Blue))
        }
    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(50, 255, 126))
            strip.setPixelColor(index, neopixel.colors(NeoPixelColors.Red))
            strip.setBrightness(10)
            index += 2
        }
    }
    strip.show()
}
```

## Finished
You have now finished your clock code. Check that your code looks exactly like below before moving on as even the slightest error in the code can cause it to not work. 

```blocks
function lights () {
    strip.clear()
    if (reset == true) {
        if (HoursOrMinutes == "Hours") {
            strip.showColor(neopixel.colors(NeoPixelColors.Green))
        } else if (HoursOrMinutes == "Minutes") {
            strip.showColor(neopixel.colors(NeoPixelColors.Orange))
        } else {
            strip.showColor(neopixel.colors(NeoPixelColors.Blue))
        }
    } else {
        index = 1
        while (index <= Math.floor(minutes / 5 * 2)) {
            strip.setPixelColor(index - 1, neopixel.rgb(50, 255, 126))
            strip.setPixelColor(index, neopixel.colors(NeoPixelColors.Red))
            strip.setBrightness(10)
            index += 2
        }
    }
    strip.show()
}
input.onButtonPressed(Button.A, function () {
    if (reset == true) {
        hours += 1
        HoursOrMinutes = "Hours"
        basic.showNumber(hours)
    }
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
input.onButtonPressed(Button.AB, function () {
    if (reset == true) {
        reset = false
        HoursOrMinutes = "None"
    } else {
        reset = true
    }
})
input.onButtonPressed(Button.B, function () {
    if (reset == true) {
        minutes += 1
        HoursOrMinutes = "Minutes"
        basic.showNumber(minutes)
    }
})
let index = 0
let HoursOrMinutes = ""
let reset = false
let strip: neopixel.Strip = null
let minutes = 0
let hours = 0
hours = 1
minutes = 0
strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB)
basic.forever(function () {
    if (reset == false) {
        basic.showNumber(hours)
        basic.pause(1)
        minutes += 1
    }
    changetime()
    lights()
})
```