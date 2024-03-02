# Autonomous driving

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

To address this problem, ...

### Use Reinforcement Learning 


### Solution architecture
There are a few key components that make this work.

For training the donkey-car simulator is used. Training in an simulator has multiple advantages. 
First you don't damage the real car when driving against a wall.

## About me
[About me](https://mariusoechslein.github.io/)
