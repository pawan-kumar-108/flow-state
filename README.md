![GitHub repo size](https://img.shields.io/github/repo-size/pawan-kumar-108/atomic-simulator)

# Atomic Simulation 
A program to simulate primitive Artificial Life using simple rules of attraction or repulsion among atom-like particles, producing complex self-organzing life-like patterns. Excluding the GUI elements, the code is less than a page. 

You don't need to understand particle physics to watch something beautiful happen. 

Just interact with the system—add energy, shift the forces, let the particles respond. Atomic Simulator turns complexity into something you can feel, not just read about.

Learn More Here (YouTube demo):
-----------------------------------------------
https://www.youtube.com/watch?v=fQvQubJ1u7E

Online Demo (JavaScript version):
-------------
Click here for a live demo (JavaScript): 
  - https://atomic-simulator.netlify.app
  
Interface (C++ version)
--------------------------------------------------------
![](images/interface.png)

Example Results
--------------------------------------------------------
![](images/big_pic.jpg)

Some Interesting Patterns to Reproduce:
-------------------------------------
You do not need to be exact with the parameters to reproduce these patterns. The best way to get interesting patterns is to first try random parameter explorations, once you find an interesting pattern, try fine-tuning it gradually. To avoid becoming stuck at a local maximum, you can make some occasional big parameter jumps. In this way interesting and different patterns shall keep poping up.

![](images/some_patterns.jpg)

To use:
-------------
Download this repo. unzip the file then go to /particle_life/bin/ folder and click on particle_life.exe

Code:
----------------
The source code is available in C++, JavaScript, and Python.

**Key Features**:
---------------

🎨 Real-Time Emergence - Watch patterns form from pure chaos in milliseconds

🔄 Adaptive Systems - Rules evolve based on what's happening in the simulation

💥 Beautiful Instability - The system thrives on breaking, not staying stable

🎮 Interactive Control - Click, drag, and modify forces in real-time

🌈 Multiple Species - Different colored particles with unique relationships

🔊 Visual Feedback - See every interaction as it happens

♾️ Never Repeats - Each session creates unique, unrepeatable patterns



**🛠️ Technical Implementation**:
---------------

Built With:

HTML5 Canvas - High-performance 2D rendering

Vanilla JavaScript - Pure JS, no frameworks needed

Physics Simulation - Newtonian attraction/repulsion forces

Spatial Optimization - Efficient particle-particle interaction calculations


The JavaScript code is as simple as this: 
-------------------------------------

```html
<canvas id="life" width="500" height="500"></canvas>
<script>
  m = document.getElementById("life").getContext("2d");
  draw = (x, y, c, s) => {
    m.fillStyle = c;
    m.fillRect(x, y, s, s);
  };
  atoms = [];
  atom = (x, y, c) => {
    return { x: x, y: y, vx: 0, vy: 0, color: c };
  };
  random = () => {
    return Math.random() * 400 + 50;
  };
  create = (number, color) => {
    group = [];
    for (let i = 0; i < number; i++) {
      group.push(atom(random(), random(), color));
      atoms.push(group[i]);
    }
    return group;
  };
  rule = (atoms1, atoms2, g) => {
    for (let i = 0; i < atoms1.length; i++) {
      fx = 0;
      fy = 0;
      for (let j = 0; j < atoms2.length; j++) {
        a = atoms1[i];
        b = atoms2[j];
        dx = a.x - b.x;
        dy = a.y - b.y;
        d = Math.sqrt(dx * dx + dy * dy);
        if (d > 0 && d < 80) {
          F = (g * 1) / d;
          fx += F * dx;
          fy += F * dy;
        }
      }
      a.vx = (a.vx + fx) * 0.5;
      a.vy = (a.vy + fy) * 0.5;
      a.x += a.vx;
      a.y += a.vy;
      if (a.x <= 0 || a.x >= 500) { a.vx *= -1; }
      if (a.y <= 0 || a.y >= 500) { a.vy *= -1; }
    }
  };
  yellow = create(200, "yellow");
  red = create(200, "red");
  green = create(200, "green");
  update = () => {
    rule(green, green, -0.32);
    rule(green, red, -0.17);
    rule(green, yellow, 0.34);
    rule(red, red, -0.1);
    rule(red, green, -0.34);
    rule(yellow, yellow, 0.15);
    rule(yellow, green, -0.2);
    m.clearRect(0, 0, 500, 500);
    draw(0, 0, "black", 500);
    for (i = 0; i < atoms.length; i++) {
      draw(atoms[i].x, atoms[i].y, atoms[i].color, 5);
    }
    requestAnimationFrame(update);
  };
  update();
</script>
```
</br>




