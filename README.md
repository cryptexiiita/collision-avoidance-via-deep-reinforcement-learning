# collision-avoidance-via-deep-reinforcement-learning

Requirement

Ubuntu 16.04.7
python2.7
ROS Kinetic
mpi4py
Stage
PyTorch

How to train

start with training in Stage 1 and when it is well-trained you can transfer to Stage 2 based on the policy model of Stage 1, this is exactly what Curriculum Learning means. Training Stage 2 from scratch may converge at a lower performance or not even converge. Please note that the motivation of training in Stage 2 is to generalize the model, which hopefully can work well in a real environment.

Please use the stage_ros-add_pose_and_crash package instead of the default package provided by ROS.

mkdir -p catkin_ws/src
cp stage_ros-add_pose_and_crash catkin_ws/src
cd catkin_ws
catkin_make
source devel/setup.bash

To train Stage1, modify the hyper-parameters in ppo_stage1.py as you like, and running the following command:

(leave out the -g if you want to see the GUI while training)
rosrun stage_ros_add_pose_and_crash stageros -g worlds/stage1.world
mpiexec -np 24 python ppo_stage1.py

How to test

rosrun stage_ros_add_pose_and_crash stageros worlds/circle.world
mpiexec -np 50 python circle_test.py

Notice

I am not the author of the paper and not in their group either. You may contact Jia Pan (jpan@cs.hku.hk) for the paper related issues. If you find it useful and use it in your project, please consider citing:

