

> From "An Introduction to AI Robotics by Robin Murphy P.5"  
> 
> A **paradigm** is a philosophy or set of assumptions and/or techniques which characterize an approach to a class of problems. It is both a way of looking at the world and an implied set of tools for solving problems.

Robotics paradigms:
- The relationship between the three primitives of robotics (SENSE, PLAN, ACT)
- How is sensory data processed and distributed through the system.

## 1.1 Hierarchical / deliberative paradigm
![An Introduction to AI Robotics by Robin Murphy p. 7](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-17-15-26-31.png =400x)

![](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-17-15-25-33.png =400x)

![](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-17-16-12-11.png =400x)

## 1.2 Reactive / Behavior-based paradigm
> From "An Introduction to AI Robotics by Robin Murphy P. 108"  
> 
> **Behaviors** are a direct mapping of sensory inputs to a pattern of motor actions that are then used to achieve a task.

![An Introduction to AI Robotics by Robin Murphy p. 7](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-18-09-37-33.png =400x)

![An Introduction to AI Robotics by Robin Murphy p. 9](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-18-09-40-06.png =400x)

![](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-17-16-11-28.png =400x)

![An Introduction to AI Robotics by Robin Murphy p. 110](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-18-10-22-14.png =400x)

## 1.3 Hybrid deliberate/reactive paradigm

![](./000_imgs/2020-06-16-Robotic-Paradigms_2020-06-18-13-12-27.png =400x)

## 1.4 Reactive architectures
Architectures provide templates for an implementation of a specific robotic paradigm.

||Subsumption|Potential Fields|
|---|---|---|
||Rodney Brooks 1986||
|**Characteristics**|1. A behavior is a network of sensing and acting modules<br/>2. Modules are grouped into layers of competence(abstract behaviors)<br/>3. Higher layers can can override, or subsume the lower layers. Behaviors operates concurrently<br/>4. No internal state (situated agent, no world model)<br/>5 Not easily taskable, need reprogramming to permorm other tasks|1.  A force field acting on the robot<br/>2. Behaviors(concurrent) are represented by vectors, emergent behavior = sum(vectors)<br/>3. Five basic potential fields: uniform, perpendicular, attractive, repulsive, and tangential<br/>5. All behaviors to be implemented as potential fields.|
|**Pros**||1. Easy to visualize the robot’s overall behavior.<br/>2. Easy to combine potential fields|
|**Cons**||1. Summation of vectors can be zero, robot stays still (local minima problem)<br/>2. Not robust<br/>3. High update rates necessary <br/>4. Parameter tuning important
|**Modularity**|High|High|
|**Niche targetability**|High|High|
|**Ease of portability**|Depends on the situation|Depends on the situation|
|**Robustness**|Low|Low|

## 2. Comparision between three robotic paradigms

|**Robotic paradigms** | Hierarchical/Deliberative paradigm | Reactive/Behavior-based paradigm | Hybrid deliberate/reactive paradigm |
| ---- | ---- | ---- | ---- |
| **Prevalent period**| 1967–1990 | 1988–1992 | 1990–present | 
| **Procedure** | 1. Sense the world<br/>2. Plan the next action<br/>3. Excecute the action | 1. Sense the world<br/>2. Act | 1.Plan<br/>2. Sense-act |
|**Characteristics**|1. Top-down procedure<br/>2. Maintain a global world model based on all sensor data |1. SENSE-ACT tight coupling<br/>2. Behavior-specific sensing  | 1. Plan(global world modeling, planning, etc.) + Sence-act<br/>2. Behavior-specific sensing + Global world models based on all sensor data.<br/>3. Planing module can share sensors with behavior modules|
| **Details**| 1. Focus on **automated reasoning and knowledge representation**<br/>2. Based on **closed world assumption** and **perfect world model** | 1. No world model, no memory<br/>2. Situated agent<br/>3. Behaviors are concurrent or sequential<<br/>4. Modular and easy-to-test behaviors||
| **Examples**| 1. Stanford CART<br/>2.Stanford Shakey<br/>3. CMU Rover  |||
| **Representative architectures** | 1. Nested Hierarchical Controller<br/>2. NIST Real-time Control System | 1. Subsumption architecture<br/>2. Potential fields architecture| 1.AuRA<br/>2. SFX<br/>3. 3T<br/>4. Saphira<br/>5. TCA|
| **Pros** |1. Ordered relationship between sensing, planning, and acting| 1. Modular and easy to test<br/>2. Incremental expansion of the capabilities of a robot<br/>3. Computationally efficient|1. Combines advantages of previous paradigms|
| **Cons** | 1. Only suitable for **fixed tailored environment**, can not deal with **unknown, unpredictable, noisy environment**<br/>2. Planning is **computational** expensive<br/>3. Can not deal with environment change while reasoning<br/>4. Optimal plans might not be necessary and might bot be optimal | 1. Robot can not perform tasks that need planning, reasoning.<br/>2. Not robust| |
| **Applications**  | Industry robotics | Law mower, vacuum cleaner | Robot navigation |

**Closed world assumption**: The world model contains everything the robot needs to know  

**Perfect world model**: The sensors are accurate, and the actions are accurate     

**Primitives of robotics**: Sense, Plan, and Act (SPA)  

**Support for modularity**: does it show good software engineering principles?

**Niche targetability**: how well does it work for the intended application?

**Ease of portability to other domains**: how well would it work for other
applications or other robots?

**Robustness**: where is the system vulnerable, and how does it try to reduce that vulnerability?

References:
1. Book: Intelligent Robots and Autonomous Agents, Robin R. Murphy, 2000
2. Slides: Introduction to mobile robotics 2020ss, University of Freibrug