

#### MSEPolicy
MLP architecture uses default config settings and recommendations from the spec:
- 3 hidden layers of size 256 followed by output layer 
- ReLU activation function between all layers

![[Pasted image 20260208001852.png]]

#### Flow Matching Policy

Loss curves are pretty similar, but it seems like the reward curve for flow matching is continually increasing over the entirety of training, whereas MSE results in the reward flattening out towards the end.

This is seen with better results observed in the videos. The final video for flow matching is extremely precise and performs the task similar to an expert, and we can also observe gradual improvement across the different videos. In the MSE videos, the final video successfully completes the task, but with some atypical movements and a lot of redundant behavior. Learning appears more erratic.

![[Pasted image 20260208003539.png]]