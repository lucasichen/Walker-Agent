## Paper Title: Emergence of Locomotion Behaviours in Rich Environments
## Paper URL: https://arxiv.org/pdf/1707.02286.pdf

## Relevant notes

## Intro

Reinforcement learning has demonstrated remarkable progress, achieving high levels of performance in Atari games, 3D navigation tasks, 
and board games. What is common among these tasks is that there is a well-defined reward function, such as the game score, which can be optimised
to produce the desired behaviour.

Reward engineering has led to a number of successful demonstrations of locomotion behaviour, however, these examples are known to be brittle: they 
can lead to unexpected results.

For starters, an environment that presents a range of challenges at various levels of difficulty can shape learning and lead it to solutions that 
would be difficult to find in more constrained settings. Second, the sensitivity to reward functions and other experiment details could be due to a type of overfitting.

Our surroundings contain a variety of obstacles of varying degrees of difficulty (e.g. steepness, unevenness, distance between gaps). 
The agent is presented with an implicit curriculum as its capabilities grow, allowing it to overcome increasingly difficult challenges.

## Large scale reinforcement with Distributed PPO

Robust policy gradients with Proximal Policy Optimization:

 ![image](https://imgur.com/8Z2fI9J.png)

Scalable reinforcement learning with Distributed PPO To achieve good performance in rich, simulated environments, we have implemented a distributed 
version of the PPO algorithm (DPPO). Data collection and gradient calculation are distributed over workers.

![image](https://imgur.com/IZNavoK.png)

## Evaluation of Distributed PPO

### Benchmark tasks

Two tasks are locomotion tasks in obstacle free environments and the third task is a planar target-reaching task that requires memory.

Planar walker: a simple bipedal walker with 9 degrees-of-freedom (DoF) and 6 torque actuated joints. It receives a primary reward proportional to
its forward velocity, additional terms penalize control and the violation of box constraints on torso height and angle.

Humanoid: The humanoid has 28 DoF and 21 acutated joints. The humanoid, too, receives a reward primarily proportional to its velocity along the x-axis,
as well as a constant reward at every step that, together with episode termination upon falling, encourage it to not fall.

Memory reacher: A random-target reaching task with a simple 2 DoF robotic arm confined to the plane. The target position is provided for the first
10 steps of each episode during which the arm is not allowed to move

## Methods: environments and models

### Training environments

In order to expose our agents to a diverse set of locomotion challenges we use a physical simulation environment roughly analogous to a platform game,
again implemented in Mujoco.

Bodies: We consider three different torque-controlled bodies, described roughly in terms of increasing complexity. Planar walker: a simple walking 
body with 9 DoF and 6 actuated joints constrained to the plane. Quadruped: a simple three-dimensional quadrupedal body with 12 DoF and 8 actuated joints.

Humanoid: a three-dimensional humanoid with 21 actuated dimensions and 28 DoF.

Rewards: For the walker the reward also includes the same box constraints on the pose as in section 2. For the quadruped and humanoid we penalize 
deviations from the center of the track, and the humanoid receives an additional reward per time-step for not falling.

Terrain and obstacles **:** (a) hurdles: hurdle-like obstacles of variable height and width that the walker needs to jump or climb over; (b) gaps: gaps in 
the ground that must be jumped over; (c) variable terrain: a terrain with different features such as ramps, gaps, hills, etc.; (d) slalom walls: walls that form
obstacles that require walking around, (e) platforms: platforms that hover above the ground which can be jumped on or crouched under.

## Results

Planar Walker: It acquired a robust gait, learned to jump over hurdles and gaps, and to walk over or crouch underneath platforms. All of these behaviors emerged
spontaneously, without special cased shaping rewards to induce each separate behaviour

![walker_image](https://imgur.com/Uu7rsrk.png)

Quadruped: The quadruped is a generally less agile body than the walker but it adds a third dimension to the control problem. Learns to navigate most obstacles 
quite reliably, with only small variations across seeds. With only minor variations across seeds, it learns to navigate most obstacles reliably. It discovers that 
jumping up or forward (with surprising accuracy in some cases) is an effective strategy for overcoming obstacles and gaps, and it learns to navigate walls, turning 
left and right as needed – despite only being rewarded for moving forward in both cases. It learns to distinguish between obstacles that it can and/or must climb over
and those that it must walk around for the variety of the hurdles-terrain.

![quad_walker](https://imgur.com/7H02Ib7.png)

#### Analyses:

For training to be successful in our setup it is required that the walker occasionally &quot;solves&quot; obstacles by chance – and the probability of this happening,
is, of course, minuscule when all hurdles are very tall. We verify this by training a Planar Walker on two different types of hurdles-terrains. The first possesses 
stationary statistics with high- and low hurdles being randomly interleaved. In the second terrain the difficulty, as given by the minimum and maximum height of the 
hurdles, increases gradually over the length of the course.

Humanoid: final set of experiments considers the 28-DoF Humanoid, a considerably more complex body than Planar Walker and Quadruped

![](https://imgur.com/j1Sy0NH.png)

In general, the humanoid presents a considerably harder learning problem largely because with its relatively large number of degrees of freedoms it is prone 
to exploit redundancies in the task specification and / or to get stuck in local optima, resulting in entertaining but visually unsatisfactory gaits. Learning
results tend to be sensitive to the particular algorithm, exploration strategy, reward function, termination condition, and weight initialization.
