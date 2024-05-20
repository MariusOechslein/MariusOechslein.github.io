# Autonomous driving

### Introduction
In the course "Embedded systems" we used Reinforcement Learning to make a JetRacer car go around a track as fast as possible.
In the end my team's car was the fastest.
I want to share a high-level overview of our solution in this blog post.

[Video of driving in the real world](https://github.com/MariusOechslein/MariusOechslein.github.io/assets/67323507/d2b8040a-0fe1-4cff-b02a-98d8359b7d56)

### Solution architecture
1. Input sensor JetRacer camera 480x480 pixels
2. Variaional Autoencoder to reduce input to 32 dimensional vector
3. Training Proximal Policy Optimization (PPO)
4. Driving in the real world

### Simulation to reality gap
We train the agent in a simulation environment for obvious reasons of money and time.
The problem is, the simulation environment is merely a simple representation of the real world, ommiting factors like road conditions, tire friction, wind, changing lighting conditions, people walking on the road, and so on.
This gap is called the simulation to reality gap.
We also encountered this problem, since we trained the agent in the simulation environment but wanted it to drive on a real track in the end.

There are many approaches to address this problem, such as domain randomization, domain adaptation, Sim-to-Real transfer, Real-World data augmentation, just to name a few.
We decided for the simple approach of reducing the dimensionality of the input space with a Variational Autoencoder.

### Variational Autoencoder
The idea of the Variational Autoencoder is the following:
1. Original image
2. Augmenting image by blurring/ overlaying/ obscurring/
3. TODO:

### Proximal Policy Optimization


### References
Kendall, A., Hawke, J., Janz, D., Mazur, P., Reda, D., Allen, J. M., ... & Shah, A. (2019, May). Learning to drive in a day. In 2019 international conference on robotics and automation (ICRA) (pp. 8248-8254). IEEE.
