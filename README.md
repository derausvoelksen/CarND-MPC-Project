# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Explanation of the Model

As given in the lesson, the state consists of the following variables:
* the x position
* the y position
* the velocity v
* the acceleration a
* the vehicle angle relative to map psi
* the steering angle of the vehicle delta
* the cross track error cte
* angle of the vehicle relative to track direction epsi

The actual state for the predicted steps depend on the reference state and the actuators applied.
Actuators (acceleration, steering) adjustment allows to reduce the model cost and result in a better trajectory.
Most of the implementation is taken from the lessen.

In order to let the vehile follow the track properly, the cost function contains the following components:
* cte: makes sure, that the vehicle actually follows the given track
* epsi: ensures, that the vehicle direction does not vary a lot
* velocity (difference to target velocity: makes sure, that the vehicle accelerates to the given speed
* all other parts are added to remove fluctuations


## Timesteps

N gives the amount of steps, that are taken into consideration. So high values of N decreases the performance of the MPC drastically. The time delta between eaech step (dt) needs also to be considered. Too large values (e.g. 0.5) did not work at all.
I came down to 0.15, and in combination of N = 15 the controller "sees" far and precise enough.

## Preprocessing

The x and y position of the vehicle needs to be transformed in to car coordinates by a translation (-x, -y) and a rotation by psi (as seen in the lesson).

## Latency

In order to deal with the latency it is necessary to shift initial inputs to the "future" by 100ms. The controller predicts the values in the same way from the next state as it was doing before.