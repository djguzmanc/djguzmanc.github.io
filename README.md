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

# Anti-aliasing (Rasterization)

## Introduction
<div style="text-align: justify">
The human kind is always researching to give more reality to computer graphics, but reality is based on a continuous world, and unfortunately the computers are not, they work on a discrete world, that means a finit resolution for all screens so, how can computers render a non horizontal or non vertical line? How can computers represent a curve with just a bunch of pixels? Do you always see pictures as this one?
</div><br>

![Alt text](/images/img.PNG)

<div style="text-align: justify">
Yo didn't right? that's because of the antialiasing algorithm, which allows us to give more reality to the pixels that represent an edge.
</div><br>

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



This techniques are commonly used for font rasterization, here is an example

![Alt text](/images/smooth_font.PNG)

This an image with a font properly rasterized, it doesn't matter which algorithm it used. Now let's see how looks the same word without antialiasing rasterization.

![Alt text](/images/no_smooth_font.PNG)



