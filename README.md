## Welcome to djguzmanc page!

I am David Guzmán, 22 years old. 

Computing engineering student at Universidad Nacional de Colombia, 4 years have passed since my first day at the university.

## Interests

<div style="text-align: justify">
When I was studying object oriented programming I wanted to develop a game as a class project, but I thought Java wasn't the best way to handle graphics, then I found Processing (2.0 at the time) and started to create my game. Probably developed 3 games that just disappear when my hard drive crashed, however I continued with Processing developing for my career projects.
</div><br>

<div style="text-align: justify">
Honestly I found graphic projects very interesting, projects that give to you the tools for building or creating things that allow you to explain or demonstrate an idea.
</div><br>

## Projects

### AlgBuilder

<div style="text-align: justify">
I'm currently working on a programming language project that allows you to create graphical animations for data structures like array o linked lists, even graphs. All graphics were handled with Processing.
</div><br>

It can be found [here](https://github.com/djguzmanc/AlgBuilder).

### Conway's Game of life editor

<div style="text-align: justify">
One day I was trying to test a shape configuration for the game of life and see its results, but online editors just offer big grids with small cells which makes it difficult to design shapes, so I started to develop this editor, allowing the user to create, save and edit shapes, even debugging generations. Made with pure Processing.
</div><br>

It can be found [here](https://github.com/djguzmanc/GameOfLife).

## Contact

Email `djguzmanc@unal.edu.co`

___

___

# Anti-aliasing (Rasterization)

## Introduction
<div style="text-align: justify">
The human kind is always researching to give more reality to computer graphics, but reality is based on a continuous world, and unfortunately the computers are not, they work on a discrete world, that means a finit resolution for all screens so, how can computers render a non horizontal or non vertical line? How can computers represent a curve with just a bunch of pixels? Do you always see pictures like this one?
</div><br>

![Alt text](/images/img.PNG)

<div style="text-align: justify">
Yo didn't right? that's because of the antialiasing algorithm, which allows us to give more reality to the pixels that represent an edge.
</div><br>

___

## State of the art

Informally the antialiasing can be defined as throwing the detail but, _carefully_. So, if you have thrown the detail how do you recover it?, well, there are a few easy techniques:

### Point sampling
It is the easiest one, but as fast as you recover an image the lower detail you get.

### Bresenham lines
Not better than point sampling, but gives more detail.

### Box filtering
Introduces the pixel gradient, removing the binary idea of a pixel ( it is black or it is white ).

### Weighted filtering
As an improvement for box filtering, ir gives a better result, but sacrifices time.

<br>

This techniques are commonly used for font rasterization, here is an example

![Alt text](/images/smooth_font.PNG)

This an image with a font properly rasterized, it doesn't matter which algorithm it used. Now let's see how looks the same word without antialiasing rasterization.

![Alt text](/images/no_smooth_font.PNG)

One may say, well, it is readable too, but serif fonts may became unredable or painfull to see.

___

## Method

Let's take a more detailed look to that algorithms described above.

### Point sampling

Let's rasterize the following line 

<img src="/images/line.PNG" width="300">

The first thing one might do is to represent this line as a rect, so we can see more easily which pixels shall we paint and which not. Don't forget that this line is represented by two points, specifying the beginning and the end of the line.

<img src="/images/line2.PNG" width="300">

Then we can choose those pixels whose centers fall inside de rect

<img src="/images/line3.PNG" width="300">

Finally if we paint that pixels we get a line, or a "line"?

<img src="/images/line4.PNG" width="300">

#### About computational performance

A line is given by the equation _y = mx + b_, the simplest aproximation is to evaluate the function for each column, then we can round that _y_ value and find the closest pixel center. The following java code shows an aproximation for this algorithm:

``` java
float fun( int x ) {
  return 0.37 * x + 1.91;
}

int[] pixelToFill( int column ) {
  int ans[] = new int[ 2 ];
  ans[ 0 ] = column;
  ans[ 1 ] = Math.round( fun( column ) );
  return ans;
}
```

We know that multiplication and rounding could be slow, so let's optimize that algorithm!. This optimization known as DDA (digital differential analyzer). Look at the following picture:

<img src="/images/ENE.PNG" width="300">

For the fourth column there are 2 options and you just need to decide between E and NE points, take a closer look and you'll note that the longest distance between the two points is 1 unit and if the line just crosses right at the middle the distance to each point may be at least 0.5. All right! we have a number decision, but how do we calc that distance value? _remember that we don't want to multiply anything!_

Look at the following equation

`>` _d = m( x + 1 ) + b - y_

If _d > 0.5_ we can decide!, for the first column, but, what about the rest of the colums? We don't need to calc anything else, just need integer steps for _x_ and _y_, it means a simple addition. The following pseudocode explains it better:

```
x = ceil( x0 )
y = round( m * x + b )
d = m * ( x + 1 ) + b – y
while x < floor( x1 )
  if d > 0.5
    y += 1
    d –= 1
  x += 1
  d += m
  output( x, y )
```
Note that we just need one multiplication for the first _d_ calc, then we use integer steps for _d_, _x_ and _y_, maybe the next image clarifies the concept...

<img src="/images/integerSteps.PNG" width="300">










