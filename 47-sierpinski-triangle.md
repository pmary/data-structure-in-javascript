# 4.7 Sierpinski Triangle

Another fractal that exhibits the property of self-similarity is the Sierpinski triangle. The Sierpinski triangle illustrates a three-way recursive algorithm. The procedure for drawing a Sierpinski triangle by hand is simple. Start with a single large triangle. Divide this large triangle into four new triangles by connecting the midpoint of each side. Ignoring the middle triangle that you just created, apply the same procedure to each of the three corner triangles. Each time you create a new set of triangles, you recursively apply this procedure to the three smaller corner triangles. You can continue to apply this procedure indefinitely if you have a sharp enough pencil.

![](/assets/recursion_03.png)

Since we can continue to apply the algorithm indefinitely, what is the base case? We will see that the base case is set arbitrarily as the minimal perimeter \(64 in this case\). Sometimes we call this number the “degree” of the fractal. Each time we make a recursive call, we cut the perimeter by one half until we reach a number below 64. When we reach a degree below 64, we stop making recursive calls.

```js
var canvas = document.getElementById('c');
var arrowCanvas = document.getElementById('a');
var context = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
arrowCanvas.width = window.innerWidth;
arrowCanvas.height = window.innerHeight;
var turtle = new Turtle(canvas, arrowCanvas);

var size = window.innerWidth/2;
var min = 64;
var pf = 0.8660254;    // Pythagoras factor: Math.sqrt(3)/2

function T(l, x, y, myTurtle) {
  // Not done yet?
  if (l > min) {
      // Scale down by 2
      l = l/2;
      // Bottom left triangle
      T(l, x, y, myTurtle);
      // Bottom right triangle
      T(l, x+l, y, myTurtle);
      // Top triangle
      T(l, x+l/2, y-l*pf, myTurtle);
  }
  // Done recursing
  else {
      // Start at (x,y)
      myTurtle.goto(x, y);
      myTurtle.down();
      // Prepare to fill triangle
      myTurtle.beginFill();
      // Triangle base
      myTurtle.forward(l);
      myTurtle.left(120);
      // Triangle right
      myTurtle.forward(l);
      myTurtle.left(120);
      // Triangle left
      myTurtle.forward(l);
      myTurtle.endFill();
      // Face East
      myTurtle.setHeading(-90);
      // Finish at (x,y)
      myTurtle.up();
      myTurtle.goto(x, y);
    }
}

turtle.setHeading(-90);
T(size, size/2, window.innerWidth/2, turtle);
turtle.draw();
```

Note that the use of recursion allows the code to reflect the structure of the picture to be drawn. Let `T` be the initial triangle \(which is invisible at first\). When we enter the function `T`, we reset the scale by one half, because the internal triangles \(that will be created next\) have half the perimeter of the original one. Then we create the bottom left triangle with `T(l, x, y)`, then the bottom right, then the top one. Then we do that to each of those triangles too – bottom left, bottom right, top – until they’re small enough, at which point we actually draw the individual triangles and fill them in with black.

Sometimes it is helpful to think of a recursive algorithm in terms of a diagram of function calls. The following diagram shows that the recursive calls are always made going to the bottom left. The active functions are outlined in black, and the inactive function calls are in gray. The farther you go toward the bottom of the diagram, the smaller the triangles. The function finishes drawing one level at a time; once it is finished with the bottom left it moves to the bottom middle, and so on.

![](/assets/recursion_diagram.jpg)

