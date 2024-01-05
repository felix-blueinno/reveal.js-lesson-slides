<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/" -->
# Today's Project

Try move around...

Try keys 1, 2, 3...

---

<!-- .slide: data-auto-animate -->
## Working Principle

1. Detect mouse movement <!-- .element: class="fragment"-->
2. Create particles if mouse is moving <!-- .element: class="fragment"-->
3. Each particle has different properties <!-- .element: class="fragment"-->
4. Shrink and fade particles over time <!-- .element: class="fragment"-->
5. Remove particle from the list when it's off-screen <!-- .element: class="fragment"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=1" -->
## 1. Detect Mouse Movement

Remember `mouseX` & `mouseY`?

```js [8-9]
function setup() {
    createCanvas(windowWidth, windowHeight);
}

function draw() {
    background(20);
    
    text(`X: ${mouseX}`, 10, 10);
    text(`Y: ${mouseY}`, 10, 20);
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
How to tell if the mouse is ***moving***?

```js [8-9]
function setup() {
    createCanvas(windowWidth, windowHeight);
}

function draw() {
    background(20);
    
    text(`X: ${mouseX}`, 10, 10);
    text(`Y: ${mouseY}`, 10, 20);
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
How to tell if the mouse is ***moving***?
> Compare previous & current position

```js [8-9]
function setup() {
    createCanvas(windowWidth, windowHeight);
}

function draw() {
    background(20);
    
    text(`pmouseX: ${pmouseX} --> mouseX: ${mouseX}`, 10, 10);
    text(`pmouseY: ${pmouseY} --> mouseY: ${mouseY}`, 10, 20);
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=2" -->
### Slow down the sketch

```js [3]
function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(1);
}

function draw() {
    background(20);
    
    text(`pmouseX: ${pmouseX} --> mouseX: ${mouseX}`, 10, 10);
    text(`pmouseY: ${pmouseY} --> mouseY: ${mouseY}`, 10, 20);
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
### Check for both axes

```diff [3, 9-10, 12-17]
function setup() {
    createCanvas(windowWidth, windowHeight);
- frameRate(1);
}

function draw() {
    background(20);
    
- text(`pmouseX: ${pmouseX} --> mouseX: ${mouseX}`, 10, 10);
- text(`pmouseY: ${pmouseY} --> mouseY: ${mouseY}`, 10, 20);

+ let isMovingX = mouseX != pmouseX;
+ let isMovingY = mouseY != pmouseY;

+ if (isMovingX || isMovingY) {
        // TODO: create particles
+ }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
### Now you should have

```js
function setup() {
    createCanvas(windowWidth, windowHeight);
}

function draw() {
    background(20);
    
    let isMovingX = mouseX != pmouseX;
    let isMovingY = mouseY != pmouseY;

    if (isMovingX || isMovingY) {
        // TODO: create particles
    }
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
### 2. Create Particles

---

<!-- .slide: data-auto-animate -->
### Create a list to store particles

```js [1]
let particles = [];

function setup() {
    createCanvas(windowWidth, windowHeight);
}

function draw() {
    background(20);
    
    let isMovingX = mouseX != pmouseX;
    let isMovingY = mouseY != pmouseY;

    if (isMovingX || isMovingY) {
        // TODO: create particles
    }
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
### Add particles to the list

```js [10-14]
...

function draw() {
    background(20);
    
    let isMovingX = mouseX != pmouseX;
    let isMovingY = mouseY != pmouseY;

    if (isMovingX || isMovingY) {
        let p = {
            x: mouseX,
            y: mouseY,
        };
        particles.push(p);
    }
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=3" -->
### Draw the particle objects

```js [17-20]
...

function draw() {
    background(20);
    
    let isMovingX = mouseX != pmouseX;
    let isMovingY = mouseY != pmouseY;

    if (isMovingX || isMovingY) {
        let p = {
            x: mouseX,
            y: mouseY,
        };
        particles.push(p);
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        circle(p.x, p.y, 10);
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=4" -->

> Try: Randomize the particle size.

---

<!-- .slide: data-auto-animate -->
### Randomize the particle size

```js [11, 18]
function draw() {
    background(20);
    
    let isMovingX = mouseX != pmouseX;
    let isMovingY = mouseY != pmouseY;

    if (isMovingX || isMovingY) {
    let p = {
        x: mouseX,
        y: mouseY,
        size: random(10, 20),
    };
    particles.push(p);
    }

    for (let i = 0; i < particles.length; i++) {
    let p = particles[i];
    circle(p.x, p.y, p.size);
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=5" -->

> Try: Make the particles move.

---

<!-- .slide: data-auto-animate -->
### Make the particles move

```js [9-10, 17-18]
function draw() {
    ...

    if (isMovingX || isMovingY) {
    let p = {
        x: mouseX,
        y: mouseY,
        size: random(10, 20),
        xSpeed: random(-5, 5),
        ySpeed: random(-5, 5),
    };
    particles.push(p);
    }

    for (let i = 0; i < particles.length; i++) {
    let p = particles[i];
    p.x += p.xSpeed;
    p.y += p.ySpeed;
    circle(p.x, p.y, p.size);
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=6" -->

> Try: Create multiple particles at once.

---

<!-- .slide: data-auto-animate -->
### Create multiple particles at once

```js [5, 14]
function draw() {
    ...

    if (isMovingX || isMovingY) {
    for (let i = 0; i < 10; i += 1) {
        let p = {
            x: mouseX,
            y: mouseY,
            size: random(5, 20),
            xSpeed: random(-5, 5),
            ySpeed: random(-5, 5),
        };
        particles.push(p);
    } // and this line❗️
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.x += p.xSpeed;
        p.y += p.ySpeed;
        circle(p.x, p.y, p.size);
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=8" -->

> Try: Shrink the particles over time.

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=7" -->
### Shrink the particles over time

```js [11, 21]
function draw() {
    ...
    if (isMovingX || isMovingY) {
        for (let i = 0; i < 10; i += 1) {
            let p = {
                x: mouseX,
                y: mouseY,
                size: random(5, 20),
                xSpeed: random(-5, 5),
                ySpeed: random(-5, 5),
                shrinkRate: random(0.5, 1.5), // ✨ new property
            };
            particles.push(p);
        }
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.x += p.xSpeed;
        p.y += p.ySpeed;
        p.size -= p.shrinkRate; // 🔄 update size
        circle(p.x, p.y, p.size);
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=8" -->

> Try: Remove particles when size < 0.

---

<!-- .slide: data-auto-animate -->
### Remove particles when size < 0

```js [17-20]
function draw() {
    ...
    if (isMovingX || isMovingY) {
        for (let i = 0; i < 10; i += 1) {
            let p = { ... };
            particles.push(p);
        }
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.x += p.xSpeed;
        p.y += p.ySpeed;
        p.size -= p.shrinkRate;
        circle(p.x, p.y, p.size);

        if (p.size <= 0) {
            particles.splice(i, 1);
            i--;
        }
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=9" -->

> Try: Randomize the particle color.

---

<!-- .slide: data-auto-animate -->
### Randomize the particle color 🎨

```js [13-15 | 26]
function draw() {
    ...

    if (isMovingX || isMovingY) {
        for (let i = 0; i < 10; i += 1) {
            let p = {
                x: mouseX,
                y: mouseY,
                size: random(5, 20),
                xSpeed: random(-5, 5),
                ySpeed: random(-5, 5),
                shrinkRate: random(0.5, 1.5),
                r: random(255),
                g: random(255),
                b: random(255),
            };
            particles.push(p);
        }
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.x += p.xSpeed;
        p.y += p.ySpeed;
        p.size -= p.shrinkRate;
        fill(p.r, p.g, p.b);
        circle(p.x, p.y, p.size);

        if (p.size <= 0) {
            particles.splice(i, 1);
            i--;
        }
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
### Better color palette 🔥

```js [1, 7 - 17]
let fireColors;

function setup() {
    createCanvas(windowWidth, windowHeight);
    noStroke();

    fireColors = [
        color("#FF0000"),
        color("#FF5A00"),
        color("#FF9A00"),
        color("#FFCE00"),
        color("#FFE808"),
        color("#FFFFFF"),
        color("#051E3D"),
        color("#052D61"),
        color("#0B1118"),
    ];
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
### Use color from the palette 🔥

```js [16 | 28]
function draw() {
    ...

    if (isMovingX || isMovingY) {
        for (let i = 0; i < 30; i += 1) {
            let p = {
                x: mouseX,
                y: mouseY,
                size: random(5, 20),
                xSpeed: random(-5, 5),
                ySpeed: random(-5, 5),
                shrinkRate: random(0.5, 1.5),
                r: random(255),
                g: random(255),
                b: random(255),
                c: random(fireColors),
            };
            particles.push(p);
        }
    }

    for (let i = 0; i < particles.length; i++) {
        let p = particles[i];
        p.x += p.xSpeed;
        p.y += p.ySpeed;
        p.size -= p.shrinkRate;
        fill(p.r, p.g, p.b);
        fill(p.c);
        circle(p.x, p.y, p.size);

        if (p.size <= 0) {
            particles.splice(i, 1);
            i--;
        }
    }
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
### More palettes 🔥 🌊 🌳

```js [2-3 | 11-17, 19-25]
let fireColors;
let waterColors;
let forestColors;

function setup() {
    createCanvas(windowWidth, windowHeight);
    noStroke();

    fireColors = [ ... ];

    waterColors = [
        color("#001b48"),
        color("#004581"),
        color("#018abd"),
        color("#97cbdc"),
        color("#dde8f0"),
    ];

    forestColors = [
        color("#4b6154"),
        color("#64ac8f"),
        color("#94d6ba"),
        color("#e7f5dc"),
        color("#c0dfc2"),
    ];
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/?stage=11" -->
### Try it out 🔥 🌊 🌳

```js [13]
function draw() {
    ...

    if (isMovingX || isMovingY) {
        for (let i = 0; i < 30; i += 1) {
            let p = {
                x: mouseX,
                y: mouseY,
                size: random(5, 20),
                xSpeed: random(-5, 5),
                ySpeed: random(-5, 5),
                shrinkRate: random(0.5, 1.5),
                c: random(fireColors), // try waterColors, forestColors
            };
            particles.push(p);
        }
    }

    ...
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/" -->

> Try: Switch palettes when keys pressed.

---

<!-- .slide: data-auto-animate -->
### 1. Record current palette ⛳️

```js [1, 5]
let currentColors;

function setup() {
    ...
    currentColors = fireColors;
}
```
<!-- .element: data-id="code" -->

____

<!-- .slide: data-auto-animate -->
### Switch palettes

```js [19]
let currentColors;

function setup() {
    ...
    currentColors = fireColors;
}

function draw() {
    ...
    if (isMovingX || isMovingY) {
        for (let i = 0; i < 30; i += 1) {
            let p = {
                x: mouseX,
                y: mouseY,
                size: random(5, 20),
                xSpeed: random(-5, 5),
                ySpeed: random(-5, 5),
                shrinkRate: random(0.5, 1.5),
                c: random(currentColors),
            };
            particles.push(p);
        }
    }
    ...
}
```
<!-- .element: data-id="code" -->
<!-- .element: class="r-stretch"-->

____

<!-- .slide: data-auto-animate -->
## Update current palette

```js
function keyPressed() {
    if (key == "1") {
        currentColors = fireColors;
    } else if (key == "2") {
        currentColors = waterColors;
    } else if (key == "3") {
        currentColors = forestColors;
    }
}
```
<!-- .element: data-id="code" -->

---

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://felix-blueinno.github.io/402D_L01_GitHub_Page/" -->

Time for some math

---

<!-- .slide: data-auto-animate -->

Names of the sides of a right triangle:
![trigo](https://gcse-math.co.uk/rhcp/wp-content/uploads/trig/sin-cos-tan.jpg)

<u>**Opp**</u>: the side opposite to the angle of interest.\
<u>**Adj**</u>: the side adjacent to the angle of interest.\
<u>**Hyp**</u>: the longest side of the triangle.

<!-- .slide: data-auto-animate -->

---

<!-- .slide: data-auto-animate -->

Names of the sides of a right triangle:
![trigo](https://gcse-math.co.uk/rhcp/wp-content/uploads/trig/sin-cos-tan.jpg)

<u>**Opp**</u>: the side opposite to the angle of interest.\
<u>**Adj**</u>: the side adjacent to the angle of interest.\
<u>**Hyp**</u>: the longest side of the triangle.

<!-- .slide: data-auto-animate -->

---

<!-- .slide: data-auto-animate -->

Identify the sides of the triangle:
![trigo](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7c/Right_Angle_Triangle.svg/2560px-Right_Angle_Triangle.svg.png)

<!-- .slide: data-auto-animate -->

---

<!-- .slide: data-auto-animate -->

Sin, Cos, Tan

<img src="https://www.mathsisfun.com/algebra/images/sin-cos-tan.svg" width="100%">

Use [calculator](https://www.google.com/search?q=sin+cos+tan+calculator&rlz=1C5CHFA_enHK1087HK1087&oq=sin+cos+tan+calculator&gs_lcrp=EgZjaHJvbWUyDggAEEUYORhDGIAEGIoFMgwIARAjGCcYgAQYigUyDAgCEAAYQxiABBiKBTIHCAMQABiABDIHCAQQABiABDIHCAUQABiABDIHCAYQABiABDIHCAcQABiABDIHCAgQABiABDIHCAkQABiABNIBCDM4MDJqMGo0qAIAsAIA&sourceid=chrome&ie=UTF-8)! (remember to change to ***deg***)

<!-- .slide: data-auto-animate -->

---

<!-- .slide: data-auto-animate -->

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://www.tldraw.com/" -->

---

<!-- .slide: data-auto-animate -->

[Kahoot](https://play.kahoot.it/v2/?quizId=6b05ed89-c202-4089-af69-9850d77ad9cc) Time!

<!-- .slide: data-auto-animate -->
<!-- .slide: data-background-iframe="https://c7bpc.csb.app/" -->

---
