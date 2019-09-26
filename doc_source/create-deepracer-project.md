# Train and Evaluate AWS DeepRacer Models<a name="create-deepracer-project"></a>

 When your AWS DeepRacer vehicle drives itself along a track, it captures environmental states with the camera mounted on the front and takes actions in response to the observations\. Your AWS DeepRacer model is a function that maps the observations and actions to the expected reward\. To train your model is to find or learn the function that maximize the expected reward so that the optimized model prescribes what actions \(speed and steering angle pairs\) your vehicle can take to move itself along the track from start to finish\. 

In practice, the function is represented by a neural network and training the network involves finding the optimal network weights given sequences of observed environmental states and the responding vehicle's actions\. The underlying criteria of optimality are described by the model's reward function that encourages the vehicle to make legal and productive moves without causing traffic accidents or infractions\. A simple reward function could return a reward of 0 if the vehicle is on the track, \-1 if it's off the track, and \+1 if it reaches the finish line\. With this reward function, the vehicle gets penalized for going off the track and rewarded for reaching the destination\. 

 For example, let's say that you're interested in having the vehicle drive without getting off a straight track\. As the vehicle speeds up and down, the vehicle may steer left or right to avoid obstacles or to remain inside\. For timed runs, you want the vehicle to go faster\. But making too big a turn at a high speed could easily lead the vehicle off the track\. Making too small a turn may not help avoid colliding with an obstacle or another vehicle\. Generally speaking, optimal actions would be to make a bigger turn at a lower speed or to steer less along a sharper curve\. To encourage this behavior, your reward function must assign a positive score to reward smaller turns at a higher speed and/or a negative score to punish bigger turns at a higher speed\. Similarly, the reward function can return a positive reward for speeding up along a straighter course or speeding down when it's near an obstacle\.

The reward function is an important part of your AWS DeepRacer model\. You must provide it when training your AWS DeepRacer model\. The training involves repeated episodes along the track from start to end\. In an episode the agent interacts with the track to learn the optimal course of actions by maximizing the expected cumulative reward\. At the end, the training produces a reinforcement learning model\. After the training, the agent executes autonomous driving by running inference on the model to take an optimal action in any given state\. This can be done in either the simulated environment with a virtual agent or a real\-world environment with a physical agent, such as an AWS DeepRacer scale vehicle\. 

 To train a reinforcement learning model in practice, you must choose a learning algorithm\. Currently, the AWS DeepRacer console supports only the proximal policy optimization \([PPO](https://arxiv.org/pdf/1707.06347.pdf)\) algorithm for faster training performances\. You can then choose a deep\-learning framework supporting the chosen algorithm, unless you want to write one from scratch\. AWS DeepRacer integrates with Amazon SageMaker to make some popular deep\-learning frameworks, such as [TensorFlow](https://www.tensorflow.org/), readily available in the AWS DeepRacer console\. Using a framework simplifies configuring and executing training jobs and lets you focus on creating and enhancing reward functions specific to your problems\. 

 Training a reinforcement learning model is an iterative process\. First, it's a challenge to define a reward function to cover all important behaviors of an agent in an environment at once\. Second, hyperparameters are often tuned to ensure satisfactory training performance\. Both require experimentation\. A prudent approach is to start with a simple reward function and then progressively enhance it\. AWS DeepRacer facilitates this iterative process by enabling you to clone a trained model and then use it to jump\-start the next round training\. At each iteration you can introduce one or a few more sophisticated treatments to the reward function to handle previous ignored variables or you can systematically adjust hyperparameters until the result converges\. 

 As with general practice in machine learning, you must evaluate a trained reinforcement learning model to ascertain its efficacy before deploying it to a physical agent for running inference in a real\-world situation\. For autonomous driving, the evaluation can be based on how often a vehicle stays on a given track from start to finish or how fast it can finish the course without getting off the track\. The AWS DeepRacer simulation runs in the AWS RoboMaker simulator and lets you run the evaluation and post the performance metrics for comparison with models trained by other AWS DeepRacer users on a [leaderboard](deepracer-racing-series.md)\. 

**Topics**
+ [Train and Evaluate AWS DeepRacer Models Using the AWS DeepRacer Console](deepracer-console-train-evaluate-models.md)
+ [Train and Evaluate AWS DeepRacer Models Using Amazon SageMaker Notebooks](train-evaluate-models-using-sagemaker-notebook.md)
+ [Input Parameters of the AWS DeepRacer Reward Function](deepracer-reward-function-input.md)