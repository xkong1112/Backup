
```
graph TD
A[Camera, Real Time]-->|Frames| B[Perception Algorithm]
C[REC, Simulation]-->|Frames| B
B-->|Blue Core, Yellow Core, Orange Core Small&Large, OpenDLV Messages| D[Path Planning Algorithm]
D-->|Steering Angle Target, Speed Target, Brake Target| E(('+/-'))
E-->F[Controller]
F-->G[EV_Cars]
G-->|SteerAngleCurrent, Speed Current, Brake Current| E


```
