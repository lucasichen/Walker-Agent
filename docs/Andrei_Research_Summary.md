## Paper Title: Teach Biped Robots to Walk via Gait Principles and Reinforcement Learning with Adversarial Critics
## Paper URL: https://arxiv.org/pdf/1910.10194.pdf

## Relevant notes

- Reinforcement learning can trains the robot to directly learn from experiences without the the requirement of the robotic model (kinematic and dynamic properties)
    - Neural network can directly map states of environment and robots to actions
    - Goal of reinforcement learning is to train a robot to learn a behaviour that will maximize the cumulative reward
- Default reward
    - Default objective of robot could be to walk as fast as possible and remain stable
        - Reward is greater for natural movement and less otherwise
- Gait reward
    - The use of only default rewards could lead to robot standing still
        - Standing is normal and stable, thus robot receives rewards
    - Gait rewards is based on a complete  gait
    - Different rewards based off of which gait phase the robot is in
- To find the optimal sub gait rewards, need to experiment with different values and perform multiple trials 
- ATD3_RNN algorithm is proposed
- Overall, this paper suggests that gait rewards, which are based on walking principles, should be implemented to assist the robot from standing still
