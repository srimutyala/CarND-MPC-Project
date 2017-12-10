# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./mpc`.

## Model
A kinematic model is used for this project using the vehicle's position (x & y), orientation(psi) and velocity(v) as its inputs. The cross-track error(cte) and orientation error(epsi) are also used. The model uses the acceleration and the steering angle change as the outputs of the actuators. The model calculates the state using the output by:

x[t+1] = x[t] + v[t] * cos(psi[t]) * dt
y[t+1] = y[t] + v[t] * sin(psi[t]) * dt
psi[t+1] = psi[t] + v[t] / Lf * delta[t] * dt
v[t+1] = v[t] + a[t] * dt
cte[t+1] = f(x[t]) - y[t] + v[t] * sin(epsi[t]) * dt
epsi[t+1] = psi[t+1] - psides[t] + v[t] * delta[t] / Lf * dt

## Timestep & Duration
We set N, the number of preited points to 10 and the time step (dt) to 0.1 secs. I started with N=25 and dt=0.05 initially and realized that the controller's predictions are having wild changes and so started changing both values until a better performance is visually achievied.

## Polynominal Fit & Transforms
We used a 3rd degree polynominal to fit the waypoints thar are transformed from map to vehicle's perspective. This shifts the origin to the reference (0,0) and the orientation angle becomes zero.

## Latency & Performance
The scaffolding code provided has a latency of 100ms which resembles real-world observations in the actuation. TThe final model uses random (arrived by traial and error) weights for the costs functions that determine how to handle magnitude of output changes, the cte error & orienttaion angle changes. These weights had an overt effect on how well the prediction tracks over the waypoints and the understeer or oversteer of the prediction. In  the end, the car drives on the track without veering off the track.
