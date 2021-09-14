# Умный бэйдж

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
Привет! Сегодня мы улучшим программу для умного бэйджа.

## Step 1 @showDialog

Найдите это место в программе:
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
### 1. Записываем имя
Поменяйте текст внутри блока ``||variables.установить значение||`` на своё имя. Бэйдж будет показывать имя, когда нажата кнопка ``|B|``.
```hint
Текст внутри блока должен быть записан на английском.
```
```block
let name = "Any other text"
```
## Step 3 @showHint
### 2. Устанавливаем время
Время устанавливается по умолчанию каждый раз, когда устройство включается. Установите текущее время с помощью команды ``||timeanddate.set time||``. Чтобы отобразить время, нажмите на сенсор над экраном.

```block
timeanddate.setTime(11, 30, 0, timeanddate.MornNight.AM)
```

## Step 4 @showHint
### 3. Меняем настроения
Это список настроений, которые может отображать бэйдж. Они отображаются при нажатии кнопки ``|A|``. Поменяйте изображения в командах ``||images.изображение значка||`` на те, которые вам нравятся.
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
### 3. Меняем настроения
Нет нужной картинки? Замените команды ``||images.изображение значка||`` на ``||images.создать изображение||`` и нарисуйте свои!

## Step 6
### 3. Меняем настроения
Нужно больше настроений? Расширьте список, нажимая кнопки ``||arrays.+||`` и  ``||arrays.-||`` и добавьте новые!

## Step 7
Все задания выполнены! Теперь, загрузите новую программу в Micro:bit и проверьте её!
