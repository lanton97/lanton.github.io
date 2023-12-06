---
layout: page
title: model-based reinforcement learning for control
img: assets/img/mbrl/husky_crop.png
importance: 3
category: fun
relevant_publications: thesis
---

This project was a component of my Masters thesis. It focussed on the development of deep model-based reinforcement learning algorithms for sample efficient robot control. This component resulted in a manuscript that is currently under review for publication. The full details and the relevant code snippets can be found in my thesis. Due to some industry partenrships, the full codebase cannot be made available. 

The code was written primarily in Python. Graphs were generated using matplotlib. The deep neural networks were constructed and trained using TensrFlow. Mathematics were done using numpy. The OpenAI Gym framework was used for environments, and the custom environments were written conforming to the Gym standard. We used the stable-baselines 3 package to compare the novel algorithm to state of the art model-free algorithms. Code for testing on the Gazebo simulation and on real robots was written using C++ and Python, with the Robot Operating System.

Inspired by the PETS algorithm, detailed in <a href="https://arxiv.org/pdf/1805.12114.pdf">this paper</a>, we decided to develop a novel shooting-based MBRL algorithm, called DVPMC, that can be used to find control inputs in real-time for use cases in robotics. These shooting-based algorithms work by first learning a predictive forward model of the system dynamics. At each time step after the model is learned, a series of actions is sampled from a distribution, and the resulting states are evaluated using a known reward function. The actions resulting in the states with the best rewards are then executed before the process is repeated. Due to the long prediction horizons necessary to determine the effects of a given action, these algorithms, although offering very high sample efficiencies, result in long computation times and require very high-accuracy models.

The key difference between our algorithm and other shooting-based algorithms was the inclusion of a learned value function that estimated the relative value of any given state. This allowed us to significantly reduce the necessary prediction horizon for our forward model. This increases computational speed and reduces the error incurred by using imperfect dynamics models autoregressively. A block diagram of the DVPMC controller can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/vimpc.png" title="DVPMC Controller" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We began by testing the algorithm on the common inverted pendulum on a cart problem. This allowed for simple debugging of the algorithm and provided a common benchmark. We trained the algorithm for 500 episodes, and compared the results to SAC and TD3, two state-of-the-art model-free RL algorithms. The training curve can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/cp_curve.png" title="Cartpole Training Curve" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We also evaluated the learned models accuracy by showing the long term prediction of the state changes against the real states. This can be seen below.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/roll2.png" title="Accuracy Evaluation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Following this, we decided to test our algorithm on a robot specific problem. We used the reach-avoid game, a type of differential game. Readers can find more details on the reach-avoid game <a href="https://fling.seas.upenn.edu/~afosr/wiki/uploads/Chaserepository/Repository/General_Reach_Avoid.pdf">here</a>. Our agent will play the invader, trying to reach a specified location before it can be captured by the opponent. The opponent will play the optimal strategy, but the game will be initialized such that the invader can alway win if it plays optimally. 

We developed a custom environment adhering to the OpenAI Gym design pattern, also implementing the optimal strategies for the opponent player. We added differential drive robot kinematics to the player to later allow us to test the learned policies on real robots.

We again train the agent for 500 episodes on the problem with randomized starting configurations to encourage generalization. We also compare against the SAC and TD3 algorithms. Thetraining results can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/ra_curve.png" title="Reach-Avoid Training Curve" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/ra_win_curve.png" title="Reach-Avoid Training Win Curve" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, we show the training curve for the reach-avoid game for multiple algorithms. On the right, we show the win rate for the same algorithms on the same training run.
</div>

As we can see, DVPMC greatly outperforms the model-free algorithms in sample efficiency.

Following this, we decided to test the learned policy on real robots. Initially, we verified the agent by testing in Gazebo. An image capture of the Gazebo simulation can be seen below.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/gazebo.jpg" title="Gazebo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Finally, we set up a real robot experiment to show the robustness of the learned policy to noise found in the real world. We used Husky differential drive robots, and a Vicom system for positioning. A diagram and a photo of the experiment setup can be seen below.
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/experiment_setup.png" title="Experiment Setup" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/mbrl/husky_crop.png" title="Robots" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

A full video of the experiments can be found <a href="https://youtu.be/0Q274kcfn4c">here</a>. Further details on the experiments and algorithms are available in my thesis, listed under the publications tab.
