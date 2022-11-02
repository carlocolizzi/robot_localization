### Computational Robotics 2022

# Neato Localization
#### Ally Bell and Carlo Colizzi


As a robot, knowing where you are accurately and quickly is a big challenge - and an important one. This project in
particular focused on the creation and implementation of a particle filter, an
algorithm that uses odometry and sensor readings to pinpoint the location of
the robot in a given map. The filter was created using Python and ROS2 on a
Neato.
After taking the odometry and LIDAR readings, the particle filter generates
a series of guesses on where the robot is inside the map. The filter itself is
initialized with a randomly distributed set of particles which represent possible
positions and orientations of the robot in the map and a guess at the robot’s
initial position. 

## Architechture and Implementation
// process diagram

### Particle Weighting

### Resampling


### Movement

Our understanding of the particles in space needs to update as the robot moves. 

## Design Descisions and Challenges

## Future Extensions

## Takeaways
Throughout this project, we wrote a lot of code without having tested any of it. Having built off the starter code, we could have made a deticated effort to be testing our code continuously as we added more and more functionality to this scaffolding. We even could have started with visiualization - enabling us to see the impacts of every step.
