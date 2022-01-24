## Paper Title: Reinforcement Learning to Run...Fast
## Paper URL: https://link.springer.com/chapter/10.1007/978-3-319-94042-7_8

## Relevant notes

- Most of this article is quite complicated in terms of the underlying mathematics used in the various algorithms, however, a lot of the main ideas are very useful 
- A general theme here is to break down the various characteristics of the motion of the humanoid so they can be individually tracked and adjusted 
    - This includes things like the x and y positions of all of the joints, the angular velocities of all of the joints, the x and y components of the centers of massses, etc. 
    - The breakdown given in the paper has 55 features
- [General] Each traning session runs until the agent falls down or takes its 1000th step 
- When trying to make a humanoid machine move, it can exploit certain features to learn quicker 
    - For example, knowing that the walking/running motion should be symmetric between the arms and legs makes predicting a good model a lot easier from the start 
        - This does need to be taken with caution
        - This only works for parts of the body that do not lie on the plane of symmetry like the head or the pelvis 
    - This greatly reduces the time required for training a good model 
- [General] The main method is to really just have random policies the model follows, train those policies, and examine if they yield within an acceptable results 
    - If they do, then you keep that policy and continue to refine it 
    - Finally you take tha refined policy and you branch outwards from there in various ways to specialize your policy