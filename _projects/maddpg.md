---
layout: page
title: MADDPG-Based Collision Avoidance
img: assets/img/marl/training_data.jpg
importance: 1
category: work
giscus_comments: true
---

In this project, we implemented an MADDPG algorithm to teach particle robot agents to coordinate without communication in order to create a formation and avoid collisions between each other and obstacles. Several variations of the environment and several learning agents were implemented, tested and compared. This project was undertaken with one other co-contributor. The project was implemented using Python. We used Tensorflow for the deep learning, numpy for mathematics, and matplotlib to generate plots, images, and animations. OpenAI Gym was used for the environment.

We implemented the MADDPG agent based on the original paper, available <a href="https://arxiv.org/pdf/1706.02275.pdf">here</a>, and a modified version of a tutorial version of <a href="https://keras.io/examples/rl/ddpg_pendulum/">DDPG</a>. We also implement an independent learning version of DDPG, where each agent learns as if in a static environment, and a version where a single DDPG agent controls all of the robots. We note that the positions of the particles, the goal and the obstacles are randomized for each trial during training and execution to encourage generalization.

Below, we depict the MADDPG training curve compared to Dec-DDPG, the independent learning agent, and the single DDPG controlling all robots.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marl/training_data.png" title="Training Curves" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Training curves of MADDPG, Dec-DDPG, and DDPG.
</div>

It is clear that MADDPG outperforms both other agents, in terms of speed of convergence, performance, and stability of convergence. 

We also perform a performance analysis below, looking at the trajectories of the robots, the relative distances of the robots from the goal, and the distance of the formation centre from the goal position over time. These can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marl/info_average_2_1.png" title="Particle Trajectories After Training" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marl/info_average_2_2.png" title="Relative Distance of Particles to Goal" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/marl/info_average_2_3.png" title="Distance of Formation Centre to Goal" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The performance of trained MADDPG agents for a single run.
</div>

More details can be seen on the Github page <a href="https://github.com/lanton97/MADDPG-Formation-Control">here</a>. The repository contains all code for the project, as well as instructions for installation and running various scenarios with different outputs.

