## Paper Title: Teaching a humanoid robot to walk faster through Safe Reinforcement Learning
## Paper URL: https://www.sciencedirect.com/science/article/pii/S0952197619302921 
This article requires you to login with your McMaster email 

## Relevant notes

This research paper mainly looks at the training of a physical robot. 

This paper mainly looks at works conducted by other groups on robot walking training, as well as this specific group's methodology as well. 

- Other Methodologies
    - Other groups use different methodologies (Deep RL, Evolutionary RL, Policy Gradient, PoWER, Q-Learning), but involve using random processes and human inputs to help with robot training. Each of these methods, as stated by Garcia and Shafie, have their own merits and flaws. One such related work invovles using a method by demonstration and correction. This method involves applying movement corrections to the walk based on the corrective feedback provided by a human, while walking autonomously using an analytical simplified walk algorithm. In this case, this requires the human to see when the robot would be about to fall and then make the correction.

- PR-SRL
    - For Garcia and Shafie, they employ Policy Reuse for Safe Reinforcement Learning  (PR-SRL) to learn the optimal locomotion walking pattern while avoid falling down, where velocity is the parameter to maximize. This algorithm uses a pre-defined configuration of a given walking behaviour as baseline policy during the learning process. In this approach, a risk function is employed to help detect dangerous situations, while also using prior knowledge during traning. By introducing the baseline policy during training, there is a fallback plan for the robot. This method, when compared to the other methods, yields results in which the robot maximizes distance travelled while minimizing the number of falls. 

- Results
    - Since this research was done with a physical robot, using a safe reinforcement learning strategy is optimal so as to minimize the number of falls, thus minimizing the amount of damage incurred on the robot. 

- Further Questions/Research:
    - One question to ask then is, how effective is a safe reinforcment learning model for a digital walker versus other state of the art algorithms. 
