---
layout: page
title: Sampling-Based Motion Planning
img: assets/img/mp/rrt.png
importance: 2
category: work
---

This is a work in progress personal project that I started to teach myself about robotic motion planning. I am implementing Python-based motion planning algorithms for mobile robots. I am focusing on writing the code in a modular, reusable way in order to make the algorithm implementations agnostic to the type of environment, obstacles and robot kinematics and dynamics.

Numpy and Python code are used to implement the algorithms and different kinematics and dynamics of the robots. PyGame is being used to generate the images and animations, allowing us to see a live view of the progress of the algorithm.

Implementation began with the creation of an empty environment with a start and end position, followed by the vizualization code. I then implemented some simple particle dynamics to simulate a basic robot.

I then began the implementations of the basic rapidly expanding random tree (RRT) algorithm. This is a sampling algorithm used to plan paths for robots. More about the algorithm can be found <a href="https://lavalle.pl/rrt/">here</a>. Essentially, RRT works by sampling random free configurations of the robot, starting with a starting position, in order to grow a tree out randomly until the tree connects to a goal position.

I implemented several variations of the RRT algorithm. I began with RRT\*, an algorithm that uses a cost metric to connect and rewire nodes in a way that minimizes the cost metric. This results in smoother paths, although it takes much longer. The RRT and RRT\* algorithms results for a simple, empty environment can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/rrt_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/rrt*_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An animation of RRT on the left, and RRT* on the right.
</div>

Following this, I implemented the bidirectional RRT and RRT\* algorithms. These algorithms work similarly to RRT and RRT\*, but grow one tree from the start position and one from the end position, until the two trees are close enough to connect. This generally reduces the amount of time needed to find a path from the start to the end.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/bd_rrt_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/bd_rrt*_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An animation of bidirectional RRT on the left, and bidirectional RRT* on the right.
</div>

I then added Dubin's curve planning and kinematics with the exisiting algorithms. I tested these on the empty environment to ensure they worked correctly. The code for the dubins kinematics themselves is a modified version of some code pulled from Github, with various modifications to make the code function with my system. Images of some of the planning can be seen below, where we can note the various curves found.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/rrt_dubins_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include gif.html path="assets/img/mp/bdrrt_dubins_run.gif" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An animation of RRT with Dubin's paths on the left, and bidirectional RRT with Dubin's paths on the right.
</div>

For the next steps, I am planning on implementing and testing collision detection and a maze environment to check the functioning of the RRT algorithms, before implementing further algorithms such as PRM and FMT. The Github page for the project is available <a href="https://github.com/lanton97/motion-planning">here</a>.
