> A **paradigm** is a philosophy or set of assumptions and/or techniques which characterize an approach to a class of problems. It is both a way of looking at the world and an implied set of tools for solving problems.
> 
> "An Introduction to AI Robotics by Robin Murphy P.5"


| Control paradigm | Hierarchical / deliberative paradigm                         | Reactive / Behavior-based paradigm                           | Hybrid deliberate/reactive paradigm |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------- |
| Time             | Late 1960s                                                   | Mid 1980s                                                    |                                     |
| Person           |                                                              |                                                              |                                     |
| Procedure        | 1. Sense the world and create the world model<br />2. Plan the next action<br />3. Excecute the action | Sensor-action couplings                                      |                                     |
| Details          | 1. Focus on **automated reasoning and knowledge representation**<br />2. Planner solver: Stanford Research Institute Problem Solver (STRIPS)<br />3. Based on **closed world assumption** and **perfect world model** | 1. No world model<br />2. Potential Field method can be used for path planning |                                     |
| Examples         | 1. Standford Shakey<br />2. Stanford CART<br />3. CMU Rover  |                                                              |                                     |
| Cases            | 1. Nested Hierarchical Controller<br />2. NIST Real-time Control System | 1. Subsumption architecture                                  |                                     |
| Pros             |                                                              | 1. Fast execution                                            |                                     |
| Cons             | 1. Only suitable for **fixed tailored environment**, can not deal with **unknown, unpredictable, noisy environment**<br />2. Planning is **computational** expensive<br />3. Can not deal with environment change while reasoning<br />4. Optimal plans might not be necessary and might bot be optimal | No planning at all                                           |                                     |
| Applications     | Industry robotics                                            | law mower, vacuum cleaner |       |

**Closed world assumption**: The world model contains everything the robot needs to know  

**Perfect world model**: The sensors are accurate, and the actions are accurate     

**Subsumption architecture**: Sub-behaviors, higher levels are able to subsume lower levels   

**Potential Field method**: repulsive force for obstacle avoidance, could fall local minimal and get stuck

**Primitives of robotics**: Sense, Plan, and Act (SPA)  



