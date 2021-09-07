# Mood Badge

```package
core
radio
microphone
proportionalFont=github:lwchkg/pxt-proportional-font
timeanddate=github:bsiever/microbit-pxt-timeanddate
```

```template
input.onButtonPressed(Button.A, function () {
    Mode = "Mood"
    if (mood == List_of_moods.length - 1) {
        mood = 0
    } else {
        mood += 1
    }
})
input.onButtonPressed(Button.AB, function () {
    Mode = "Heart"
})
input.onButtonPressed(Button.B, function () {
    Mode = "Name"
})
input.onGesture(Gesture.Shake, function () {
    Mode = "Oracle"
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    Mode = "Watch"
})
let mood = 0
let Mode = ""
let List_of_moods: Image[] = []
let name = "Your name"
timeanddate.setTime(11, 30, 0, timeanddate.MornNight.AM)
List_of_moods = [
images.iconImage(IconNames.Silly),
images.iconImage(IconNames.Happy),
images.iconImage(IconNames.Sad),
images.iconImage(IconNames.Confused),
images.iconImage(IconNames.Angry),
images.iconImage(IconNames.Fabulous),
images.createImage(`
    . . # . .
    . # . # .
    . . . # .
    . . # . .
    . . # . .
    `)
]
Mode = "Heart"
basic.forever(function () {
    if (Mode == "Heart") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 1)
        basic.showIcon(IconNames.Heart)
        pins.digitalWritePin(DigitalPin.P1, 0)
        basic.showIcon(IconNames.SmallHeart)
    } else if (Mode == "Mood") {
        pins.digitalWritePin(DigitalPin.P0, 1)
        pins.digitalWritePin(DigitalPin.P1, 0)
        List_of_moods[mood].showImage(0)
    } else if (Mode == "Name") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 1)
        basic.clearScreen()
        proportionalFont.showString("" + name + "   ", 200)
    } else if (Mode == "Watch") {
        basic.clearScreen()
        proportionalFont.showString("" + timeanddate.time(timeanddate.TimeFormat.HMMAMPM) + "   ", 200)
    } else if (Mode == "Oracle") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 0)
        images.createBigImage(`
            . . . . # # # # # #
            . . . # # # # # # #
            . . # # # # # # # #
            . # # # # # # # # #
            # # # # # # # # # #
            `).scrollImage(1, 200)
        if (Math.randomBoolean()) {
            pins.digitalWritePin(DigitalPin.P0, 1)
            basic.showIcon(IconNames.Happy)
        } else {
            if (Math.randomBoolean()) {
                pins.digitalWritePin(DigitalPin.P1, 1)
                basic.showIcon(IconNames.Sad)
            } else {
                basic.showString("?")
            }
        }
        basic.pause(2000)
        if (Mode == "Oracle") {
            Mode = "Heart"
        }
    }
})
```

```blocks
input.onButtonPressed(Button.A, function () {
    Mode = "Mood"
    if (mood == List_of_moods.length - 1) {
        mood = 0
    } else {
        mood += 1
    }
})
input.onButtonPressed(Button.AB, function () {
    Mode = "Heart"
})
input.onButtonPressed(Button.B, function () {
    Mode = "Name"
})
input.onGesture(Gesture.Shake, function () {
    Mode = "Oracle"
})
input.onLogoEvent(TouchButtonEvent.Pressed, function () {
    Mode = "Watch"
})
let mood = 0
let Mode = ""
let List_of_moods: Image[] = []
let name = "Your name"
timeanddate.setTime(11, 30, 0, timeanddate.MornNight.AM)
List_of_moods = [
images.iconImage(IconNames.Silly),
images.iconImage(IconNames.Happy),
images.iconImage(IconNames.Sad),
images.iconImage(IconNames.Confused),
images.iconImage(IconNames.Angry),
images.iconImage(IconNames.Fabulous),
images.createImage(`
    . . # . .
    . # . # .
    . . . # .
    . . # . .
    . . # . .
    `)
]
Mode = "Heart"
basic.forever(function () {
    if (Mode == "Heart") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 1)
        basic.showIcon(IconNames.Heart)
        pins.digitalWritePin(DigitalPin.P1, 0)
        basic.showIcon(IconNames.SmallHeart)
    } else if (Mode == "Mood") {
        pins.digitalWritePin(DigitalPin.P0, 1)
        pins.digitalWritePin(DigitalPin.P1, 0)
        List_of_moods[mood].showImage(0)
    } else if (Mode == "Name") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 1)
        basic.clearScreen()
        proportionalFont.showString("" + name + "   ", 200)
    } else if (Mode == "Watch") {
        basic.clearScreen()
        proportionalFont.showString("" + timeanddate.time(timeanddate.TimeFormat.HMMAMPM) + "   ", 200)
    } else if (Mode == "Oracle") {
        pins.digitalWritePin(DigitalPin.P0, 0)
        pins.digitalWritePin(DigitalPin.P1, 0)
        images.createBigImage(`
            . . . . # # # # # #
            . . . # # # # # # #
            . . # # # # # # # #
            . # # # # # # # # #
            # # # # # # # # # #
            `).scrollImage(1, 200)
        if (Math.randomBoolean()) {
            pins.digitalWritePin(DigitalPin.P0, 1)
            basic.showIcon(IconNames.Happy)
        } else {
            if (Math.randomBoolean()) {
                pins.digitalWritePin(DigitalPin.P1, 1)
                basic.showIcon(IconNames.Sad)
            } else {
                basic.showString("?")
            }
        }
        basic.pause(2000)
        if (Mode == "Oracle") {
            Mode = "Heart"
        }
    }
})
```
## Step 0 @showDialog
Hello! This is a program for your Mood Badge. Let's modify it!

## Step 1 @showDialog

For your badge to function properly, you should input your name and the current time. Also, you can change the displayed moods. First, find this place in the code:
```blocks
let name = "Your name"
timeanddate.setTime(11, 30, 0, timeanddate.MornNight.AM)
List_of_moods = [
images.iconImage(IconNames.Silly),
images.iconImage(IconNames.Happy),
images.iconImage(IconNames.Sad),
images.iconImage(IconNames.Confused),
images.iconImage(IconNames.Angry),
images.iconImage(IconNames.Fabulous),
images.createImage(`
    . . # . .
    . # . # .
    . . . # .
    . . # . .
    . . # . .
    `)
]
```
## Step 2 @showHint
### 1. Setting the name
Change the text inside the ``||variables.set||`` block to be your name. This text will be shown when the ``|B|`` button is pressed.
```hint
You can type anything other than your name instead.
```
```block
let name = "Any other text"
```
## Step 3 @showHint
### 2. Setting the current time
The time is reset every time when your device is turned on. You can set it with the ``||timeanddate.set time||`` block. To see the current time, press the Micro:bit logo.
```hint
Fill in the hours, minutes and seconds.
Also, you can switch between AM and PM. 
```
```block
timeanddate.setTime(11, 30, 0, timeanddate.MornNight.AM)
```

## Step 4 @showHint
### 3. Changing moods
This is a list of moods that your badge can show. Moods can be displayed and switched with the ``|A|`` button. Feel free to change the pictures inside the ``||images.icon image||`` blocks to get the set of moods that you like.
```block
List_of_moods = [
images.iconImage(IconNames.Silly),
images.iconImage(IconNames.Happy),
images.iconImage(IconNames.Sad),
images.iconImage(IconNames.Confused),
images.iconImage(IconNames.Angry),
images.iconImage(IconNames.Fabulous),
images.createImage(`
    . . # . .
    . # . # .
    . . . # .
    . . # . .
    . . # . .
    `)
]
```

## Step 5
### 3. Changing moods
To customize these moods even more, you can replace some (or even all) of the ``||images.icon image||`` blocks with ``||images.create image||`` blocks and fill in your own pictures!

## Step 6
### 3. Changing moods
Want to display more moods? You can expand or shrink your list with ``||arrays.+||`` and  ``||arrays.-||`` and add new moods to your list!

## Step 7
Completed all the tasks? Awesome! Download the code to your Micro:bit and check its new behaviour!
