# Autonomous driving //Blog post is under construction

In this project, I trained a Jetracer car to drive fully autonomously around a track in real life. 
The training is done with Reinforcement Learning within a simulation environment.
The real driving is done on waveshare mat with a simple O-shaped track.
Here's a video of the end result: 

[Jetracer Autonomous Driving video](https://github.com/MariusOechslein/MariusOechslein.github.io/assets/67323507/c96bf23c-c210-4d42-97ee-cfd6dd95bd84)

This blog post covers the most important components we implemented in order to make the car drive autonomously.
At the end I will also discuss the limitations of this approach.

### Problem statement 
The problem statement we were given at the start of the semester included:
- Train the car within a simulation environment
- Use Reinforcement Learning
- The only sensor input we can use is the camera that is mounted onto the car

In the following sections I will go into more detail on each of these points.

### Simulation environment
We trained the car within a simulation environment. This has multiple advantages but also one major disadvantage.

On the one hand, the big advantages are that nothing can be damaged within the simulation environment, which is especially important for the first few training episodes when the car hasn't learned to avoid obstacles yet.
Also, no human is needed to stop the car or put it back into the starting position - in the simulation, the car is just reset to the starting position when hitting a wall.
This means that the car can learn to drive as long as needed without the need for human intervention or the risk of damaging something.

The major disadvantage on the other hand is the resulting simulation to reality gap. The issue is that the simulation environment will most likely look different from the real world.
For example, the reality introduces variations in lighting, surface of the track, wheel resistance, battery life, people standing around the track, just to name a few.
This results in the problem that the ability to perfectly drive in the simulation environment may not translate to the real world.

### Addressing the "reality gap"
The research branch "simulation-to-reality" proposes multiple approaches for handling this problem.

There are also other, more sophisticated approaches to address the problem of [simulation-to-reality](https://blog.research.google/2017/10/closing-simulation-to-reality-gap-for.html#:~:text=The%20difficulty%20of%20transferring%20simulated,enabling%20effective%20real%2Dworld%20performance.).
In this research by google ...

A research group at [Nvidia](https://developer.nvidia.com/blog/transferring-industrial-robot-assembly-tasks-from-simulation-to-reality/) solved it by ...

In our project we used domanin randomization and dimensionality reduction to reduce the reality gap.
We did this by an Variational Auto-Encoder.       // TODO: Citation
The underlying architecture behind an Autoencoder is an encoder, a latent space, and a decoder.
Both encoder and decoder are simple neural networks. The encoder has a higher higher-space than output-space, while the decoder has a lower input-space than output-space. 
This results in a latent space between the encoder and decoder which has a information-dense representation of the input. 
The goal of the Autoencoder is to recreate the original image and it is therefore trained by comparing the input into the Encoder with the output of the Decoder. Normally Mean squared error is used as the loss function.
The idea is that when the Autoencoder is able to recreate the original image the latent space between the Encoder and Decoder must have a information-dense representation of the input, with lower dimensions than the input - which is the Dimensionality Reduction we apply.

In our case the original image's dimensions are 128x128x3 which results in 49.152 dimenions.
The output of the Encoder only has 32 dimensions.
Of course this immense reduction of dimensions suggests a lot of information loss and information will surely be lost in the process.
But the main idea of the Autoencoder is to represent the important information of the image in as little dimensions as possible.
This means that the information of the image is very densely represented in the vector with 32 dimension while the information in the 49.152 dimensions of the image is not as dense.
Of course information will be lost, but the hope is to pretain the most important information like where the road lines are, where the middle of the road is, if the next corner goes to the right or left, and how far away the next corner is.

The Variational Autoencoder extends this architecture by adding preprocessing (mainly noise) to the input-images.
In our case, we cropped away the top 20% of the image so the resulting image only contains the road and not the background.
Additionally we augmented the input image by adding noise, blurring, color-jittering, ...
The goal of the Variational Autoencoder is still to recreate the original image before the preprocessing.
This makes the resulting latent-space between the Encoder and Decoder more robust, since the Autoencoder has to learn the important features of the images while disgarding the noise to be able to recreate the original image as closely as possible.

### Use Reinforcement Learning
For training our Reinforcement Learning method, also encode the images with the trained Encoder and use this information-dense lower-dimensional representation as the state of the environment.
This helps training the Reinforcement Learning method in multiple ways. 

First, it's faster for the Reinforcement Learning method to train with a state of 32 dimensions than with a state of 49.152 dimensions, simply because it's less dimensions.
Second, 




### Solution architecture
There are a few key components that make this work.

For training the donkey-car simulator is used. Training in an simulator has multiple advantages. 
First you don't damage the real car when driving against a wall.

## Resources
- Variational Autoencoder paper: Kingma, D. P., & Welling, M. (2013). Auto-encoding variational bayes. arXiv preprint arXiv:1312.6114.
- Variational Autoencoder: https://www.ibm.com/de-de/topics/autoencoder

## About me
[About me](https://mariusoechslein.github.io/)
