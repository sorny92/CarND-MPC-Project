# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

#### 1.  Student describes their model in detail. This includes the state, actuators and update equations.
Based on the information received from the course and the Q&A video, I've created a model which can lap around the circuit without problems.
The equations which I used to create the cosntrains of the models are based on the next:
![model](https://github.com/sorny92/CarND-MPC-Project/blob/master/model.jpg)

#### 2.  Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.
N and dt values have been chosen based on a try & error method. I tried different values of N and dt. When I increased dt the response was to slow to make the car follow the path. When it was too high it responded to fast for the latency it had so it end up having erratic trajectories.
When N was too low, this wasn't enough information to predict the control on time in turns. When I was too high the responses it wanted to do it didn't make sense at low speeds, also the computational cost was high.

#### 3.  If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.
In the first try I didn't have any preprocessing in the input data and I only used global coordinates, then the output was transformed into car coordinates, but after I could make it work I did the transformation of the coordinates from global to car before sending this coordinates to the MPC.
That's the only preprocessing applied to the model.

#### 4.  The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.
The problem of latency is that the car needs time to respond to a change so if you had a control which actuates more than the latency time what can happen is to compute more than it's actually need. Because of latency you will find yourself late to respond to an input. A way to solve it is softening your actions to make your changes (but not too much) softer so you can avoid jumping between values.
