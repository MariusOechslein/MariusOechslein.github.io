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
The simulation environment is merely a simple representation of the real world, ommiting factors like road conditions, tire friction, wind, changing lighting conditions, people walking on the road, and so on.
This gap is called the simulation to reality gap.
The problem is that the agent learns to act in the simulation environment but this knowledge might not transfer to the real world, since the states simply look different.
We also encountered this problem, since we trained the agent in the simulation environment but wanted it to drive on a real track in the end.

There are many approaches to address this problem, such as domain randomization, domain adaptation, Sim-to-Real transfer, Real-World data augmentation, just to name a few.
We decided for the simple approach of reducing the dimensionality of the input space with a Variational Autoencoder.
This helps in multiple ways:
- Reduced complexity of the environment, since the states only have 32 dimensions and not 480x480 = 230.400.
- Robustness and Noise reduction, since only the most important features of the image are captured in the latent space.
- Efficient learning, since there are fewer states the agent has to train on.

### Variational Autoencoder
The idea of the Variational Autoencoder is the following:
1. Original image
2. Augmenting image by blurring/ overlaying/ obscurring/ ...
3. Encoder network with 32 dimensional output space (latent space)
4. Decoder network with an output the same dimensions as the original image

The Autoencoder is trained by comparing the output image from the Decoder with the original image with MSE (Mean Squared Error).
The Variational Autoencoder has two main benefits:
- Dimensionality reduction to a information-rich latent space
- Unsupervised training


### References
Kendall, A., Hawke, J., Janz, D., Mazur, P., Reda, D., Allen, J. M., ... & Shah, A. (2019, May). Learning to drive in a day. In 2019 international conference on robotics and automation (ICRA) (pp. 8248-8254). IEEE.
