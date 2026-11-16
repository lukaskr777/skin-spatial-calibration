# Skin Spatial Calibration via Pressure Correlation Measurements

A research project I did at Maastricht University (Department of Advanced Computing Sciences) in 2023.

**Paper:** [MARBLE_Paper.pdf](MARBLE_Paper.pdf)

## The problem

A robot covered in soft skin has many pressure sensors, but it does not know where each sensor sits on its body. Without that map it cannot tell what shape is touching it. Measuring every sensor position by hand does not scale.

## What I did

I built two algorithms that work out the sensor layout from pressure readings alone, with no extra hardware.

The idea is simple: when a small object slides over the skin, sensors that light up at the same time must be close to each other.

- **Algorithm I** starts from random positions and nudges sensors closer or further apart after each new frame of data. Positions slowly freeze as confidence grows. It is designed to keep updating while the robot is in use.
- **Algorithm II** turns pressure readings into distance estimates between sensor pairs, then places the sensors one by one with probabilistic multilateration. This method is borrowed from wireless sensor network localization.

## Results

Tested in simulation on 100 sensors spread over a 10 x 10 unit area, in grid and random layouts:

| Method | Average position error |
| --- | --- |
| Random guess | about 4.3 units |
| Algorithm I | down to about 1 unit |
| Algorithm II | down to about 0.6 units |

Both methods recover the relative layout well. Absolute distances are less reliable, and accuracy drops with large or oddly shaped objects. The work covers 2D layouts only.

## About the code

The code lives in a private repository, which holds the hardware side of the project:

- Arduino firmware for a soft-skin arm with 80 pressure sensors on three skin patches, plus joint angle encoders
- Python scripts to record the sensor data and replay it as a live pressure map
- Recorded datasets with the arm at different angles

The people who built the arm and the simulation are credited in the paper.

## Author

Lukáš Krajčík
