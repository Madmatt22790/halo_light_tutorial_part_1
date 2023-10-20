# Halo Light Clock
## Introduction
In this tutorial we are going to create a clock program for our micro:bits that have a Halo Light ring connected to them.

If you ever get stuck with what your code should look like check out the hint in the bottom left corner of this tutorial. 
```
Hints will be displayed in here.
```
## Step 1
A variable is used to store different kinds of information. It can store information such as number, words, lists, or booleans to name a few.

We need to create 2 such ``||variables: variables||`` to start
 - ``||variables: hours||``
 - ``||variables: minutes||``

Select the ``||variables: variables||`` section then choose "Make a Variable" and name it ``||variables: hours||`` then do the same for ``||variables:minutes||``.

## Step 2
With the variables created we need to set what their starting values are going to be.
Drag the ``||variables.set minutes to 0||`` into the start block
The dropdown menu can be used to swap between your variables. 

Do this again but switch the variable to ``||variables: hours||`` and change its starting value to 1.
```blocks
let minutes = 0
let hours = 1
```

## Step 3
Now we need to display the hours variable on the LEDs.
Do this by dragging a ``||basic.showNumber||`` block into the forever loop then place the ``||variables: hours|`` variable inside of it.

```blocks
basic.forever(function () {
    basic.showNumber(hours)  
})
```

## Step 4
Next we need to increase the ``||variables:minutes||`` variable by 1 every 60 seconds.

We do this by having the forever loop pause for 60 seconds before adding 1 to the variable.
Drag a ``||basic.pause (ms)||`` block and place it after the show number block in the forever loop.
Change the number within this block to 60000 as that is how many milliseconds are in a minute.

```blocks
basic.forever(function () {
    basic.showNumber(hours) 
    basic.pause(60000) 
})
```

## Step 5
Now add a ``||variables: change minutes by 1||`` block underneath the pause block.
This will increase the minutes variable by 1 after the program has paused for 1 minute.

```blocks
basic.forever(function () {
    basic.showNumber(hours) 
    basic.pause(60000)
    minutes += 1
})
```

## Step 6
There are two more things to do before the clock portion of the program works
   1. Increase ``||variables: hours||`` variable by 1 whenever the ``||variables:minutes||`` variable gets to 60
   2. When the ``||variables: hours||`` variable gets to 13 to change it back to 1 to start the loop all over again.

We are going to do this by creating a custom code block to handle both of these at the same time. 

The reason we would use a custom code block is that it keeps our code neater and easier to read. 

Select Advanced then choose Functions before pressing Make a Function.

In the pop up the default name for the function will be doSomething. 

Change this to changeTime. 

Finally select Done and your function will appear in the workspace.
```blocks
function changeTime () {}
```

## Step 7
If you select the Functions section again you will now see that there are two new blocks
  - ``||functions: return||``
  - ``||functions: call changeTime||``

We are only concerned with the ``||functions: call changeTime||`` block as this is what will be placed within the forever loop to run the code inside the Function block we just created.

Drag this block and place it underneath the block that increases our minutes variable by 1.
```blocks
function changeTime () {}

basic.forever(function () {
    basic.showNumber(hours) 
    basic.pause(60000)
    minutes += 1
    changeTime()
})
```

## Step 8
Next lets look at what we want the changeTime function to do when it is called in the forever loop. 

We are going to need to use a couple of ``||logic: if||`` blocks to help our code make decision.

Drag two of these into our changeTime function.
```blocks
function changeTime () {
    if (true) {})
    if (true) {})
}
```

## Step 9
Whatever we put inside one of the ``||logic: if||`` blocks will be run when the condition is true. By default it is always true but we need to change that. 

We want to check the minutes variable value and see if it is equal to 60.

To do this drag a ``||logic: 0 = 0||`` block and place it in the if statement where it currently says true.

Then drag the ``||variables: minutes||`` variable and place it to the left of the equals sign. 

Lastly change the 0 on the right of the equals sign to 60.

Now whatever we put inside this ``||logic: if||`` block will only run if the ``||variables: minutes||`` variable is equal to 60.
```blocks
function changeTime () {
    if (minutes == 60) {})
    if (true) {})
}
```

## Step 10 
Within this if statement drag a ``||variables: change hours by 1||`` and a ``||variables: set minutes to 0||``

This will reset the minutes variable back to 0 and increase the hours variable by 1.

```blocks
function changetime () {
    if (minutes == 60) {
        hours += 1
        minutes = 0
    }
    if (true) {}
}
```

## Step 11
Lets do the same thing to the second ``||logic: if||`` block but instead checking if the ``||variables: hours||`` variable is equal to 13 and setting it to 1 if that is true.

```blocks
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

## Part 1 Complete
That is it for the first part of this tutorial. Check your code to make sure it is the same as in the hint.

Part 2 can be found here.
```blocks
let minutes = 0
let hours = 1
```
```blocks
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

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
