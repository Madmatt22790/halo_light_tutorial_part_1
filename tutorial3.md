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

