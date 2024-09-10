### Simple G-Force Components

A method for approximating the acceleration along each local axis of certain vehicles, mainly standard ground vehicles and fixed-wing aircraft in SimplePlanes. The total acceleration in Gs is the sum of the static and dynamic sources of acceleration shown below.

**Assumption:**
The angles of attack and slip are small, meaning that the x- and y-components of velocity are small. In addition, the z-component can be assumed to be always positive on airplanes. Therefore, on an airplane, the z-component of the velocity is approximately equal to ground speed (GS).

### Static Components

The static component comes solely from the machine's pitch and roll angles. Gravitational acceleration, which points down in world space, acts on the vehicle at all times and attempts to bring it into a state of free fall. The static component of acceleration here represents the acceleration that must be applied to the vehicle to counteract gravitational acceleration, and maintain a state of equilibrium, like when the vehicle is parked or flying in a straight line.

The static component can be mapped to the local axes of the vehicle as shown:

- x: `cos(PitchAngle) * sin(RollAngle)`
- y: `cos(PitchAngle) * cos(RollAngle)`
- z: `sin(PitchAngle)`

It can also be seen that the value on an axis is positive if the up vector (0, 1, 0) points in that direction. In addition, the magnitudes of the static component of acceleration and the up vector are both equal to 1.
