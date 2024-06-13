## 1. Introduction

Active ragdolls are today's game development feature that fuses the dynamic physical interactions of ragdoll physics with the structured movements of predefined animations. In this manner, active ragdolls will permit characters to behave more lifelike and responsive under various game scenarios, surely augmenting the player's immersion and engagement. Implementing active ragdolls in combination with animations in Unity is a unique set of opportunities and challenges, making this an exciting topic whether we are looking to make our models more realistic or more wacky, however preferred.


### 1.1. What is an Active Ragdoll?

An active ragdoll is a hybrid approach to character control, trying to mix the dynamics of a Rigid body physics–founded ragdoll with key-framed animations. But unlike the usual ragdolls, relying purely on physical forces, an active ragdoll contains animations to preserve the necessary motions of a character, allowing realistic physical behavior towards actions performed on the character. This gives a chance for the move from controlled animation to dynamic response—like hitting obstacles—to be hit or falling to become more believable and organic in nature.


## 2. Challenges in Implementing Active Ragdolls

### 2.1. Balancing Animation and Physics

One of the biggest challenges in implementing active ragdolls is finding the right balance between physics and animation. The active ragdoll has to maintain desirable animations but also show natural response to physical forces. Too much priority can be given to animation, leading to stiff character behavior, or too much to physics, leading to improper movements of the character.




### 2.2. Optimizing Performance

Active ragdolls can be very performance-heavy, as they require a lot of continuous calculations to blend the physics interaction with animations. The optimization of performance in order to maintain smooth gameplay plays a big role, especially on low-end hardware. This is about efficient use of the physics engine within Unity, optimizing collision detection and minimizing computational load through techniques like LOD for physics calculations.


### 2.3. Smooth State Transitions

It is very important to make transitions between the animation states and the rag doll states smooth to keep the illusion of a coherent character. The player will lose his immersion if the change is too noticeable or other artifacts will make their appearance. Needed techniques for this are those of interpolating animations over time, inverse kinematics, and joint constraints.


### 2.4. Stability and Control

The maintenance of stability and control of the character during the active ragdolling of characters seems to be one of the challenges that arise. It means the characters should be able to get up in case of a fall or a hit where it is not acting in a too constraining way or weirdly. Trickled with strong control algorithms like PD controllers or other feedback mechanisms, stable and controlled ragdoll behavior can be implemented.






## 3. Implementation and Parameters

I started by rigging a selected model’s each limb individually on a model mesh (Figure 1) and then added several components for every single one (Figure 2). Those said components were my main focus parameters for this project.


![image](https://github.com/user-attachments/assets/9c3ebfe2-0d77-4f00-b7f0-51962b92aae5)    
Figure 1: Rigged limbs with their custom colliders



![image](https://github.com/user-attachments/assets/18b7ba56-2a0f-46dc-a43e-4e426ee5527f)    
Figure 2: Added components on spine part


Mass is one of the crucial parameters. Every limb has to have its own distinctive mass just like in real life and they have to distribute the overall mass of our model across proportionately. (Figure 3) Colliders, mostly capsule and box, work along with rigidbodies to detect collisions once any occur. They have to represent the overall shape of a given limb individually and pile up to scale to the whole body. (Figure 4)

![image](https://github.com/user-attachments/assets/8b28d585-5ebf-424b-afa3-0614e63c015a)    
Figure 3: Rigidbody controlling mass  


![image](https://github.com/user-attachments/assets/6c4fa792-476b-49e5-88e5-05e0954514d1)    
Figure 4: Capsule collider of a limb


Configurable joints contain arguably the most important factors. Spring values and motion swing locking are extremely crucial to get a working physics for a model. Motion locking, along with connected body parts, prevents the limbs from going too further away from the base model and even acting on their own as if they are not a part of the body. (Figure 5)



![image](https://github.com/user-attachments/assets/1ba00f4f-f948-4edf-939c-862cbb26f7ae)    
Figure 5: Configurable joint of a limb


If the spring values are set too low, libs will lose their rigidity, making the model collapse under its mass. (Figure 6) And if they are set too high they will become too stiff and way less reactive towards physical forces affecting them such as hits, motion, momentum, inertia etc and will make them act almost like a traditionally animated model, depending on how high those values are set.


![image7](https://github.com/user-attachments/assets/d9e022c7-96e0-4eca-a9dd-2b4022dfc6e9)    
Figure 6: Low spring values and low rigidity values resulting in a similar function to traditional passive ragdolls


After all that is done we need to import animations to our physics model by targeting a static animation model through a script. (Figure 7 and 8)



![image1](https://github.com/user-attachments/assets/9286f9aa-66c1-47c1-a2f4-e77e6d4fb2d3)    
Figure 7: Jiggle physics on an unanimated mesh next to our animation target



![image10](https://github.com/user-attachments/assets/24e6eb3c-5d6f-4342-9777-3b708b9211d3)    
Figure 8: Previously unanimated physics mesh copying animations from the target animation mesh and blending both with physics interactions


From this point on, unfortunately, I couldn’t continue with our little cat model because I had to demonstrate the limbs other than just the head working being affected by physical forces in a clear manner. So I switched it to a mannequin model which allows the demonstration of legs and arms reacting to physical forces as well. I proceed with creating a scene where our physics model is replaced by a mannequin. And a copy of it just using a static animation mesh to demonstrate how they act differently from each other. (Figure 8) Note that every other thing including the controller are the exact same. The only difference being, one employs ragdoll physics and the other doesn’t.


![image12](https://github.com/user-attachments/assets/cb56b5b7-5164-4a26-b1aa-1bd46812d6db)    
Figure 9: An active ragdoll finding its way through a limbo stick while a traditional animated model failing and falling over

## 4. Performance Tests and Conclusions

I proceeded with creating a new scene where I can test the performance of active ragdolls in a couple of scenarios (Figure 9). This section will include the results from those tests. All tests were made in exactly the same conditions except the model type where spawn intervals are 0.5 seconds and a total of 100 spawns. Our performance metrics will be CPU and memory usage and physics metrics. We will take the peaking spike points and compare them to evaluate the performance.


![image4](https://github.com/user-attachments/assets/84cc1d19-8b53-48ed-9ba9-73e15746d637)    
Figure 10: Performance test platform


### 4.1 Test 1: Active Ragdolls


![image](https://github.com/user-attachments/assets/145179c2-5af8-4412-88eb-6b53f845b4e4)    
Figure 11: Performance graph of active ragdolls


### 4.2 Test 2: Active Ragdolls Without Animations


![image](https://github.com/user-attachments/assets/6cda5660-c173-41c2-823f-284fa6c4dd09)    
Figure 12: Performance graph of active ragdolls without animations


### 4.3 Test 3: Passive Ragdolls


![image](https://github.com/user-attachments/assets/205b0675-0011-4595-85ec-6b279ec66c16)    
Figure 13: Performance graph of passive ragdolls


### 4.4 Test 4: Animated Model Without Ragdoll Physics

![image](https://github.com/user-attachments/assets/53833978-3cb3-4c7d-b70e-131aff83bdf0)    
Figure 14: Performance graph of animated model without ragdoll physics


### 4.5  Test 5: Plain Mesh


![image](https://github.com/user-attachments/assets/99ff1850-3fba-41b6-bb87-35da573d79f8)    
Figure 15: Performance graph of plain mesh


### 4.6 Performance Evaluation

This section presents the analysis of memory usage and FPS values across different tests, taking Test 5 as the baseline for comparison. All values used are taken from peaking spikes.

| Test | Memory (GB) | FPS | Memory Usage (%) | FPS Increase (%) |
| :---: | :---: | :---: | :---: | :---: |
| 1 | 1.63 | 100.0 | 167.21% | \-96.67% |
| 2 | 1.25 | 500.0 | 104.92% | \-83.33% |
| 3 | 1.54 | 250.0 | 152.46% | \-91.67% |
| 4 | 0.63 | 800.0 | 3.28% | \-73.33% |
| 5 | 0.61 | 3000.0 | 0.00% | 0.00% |    
Figure 16: Summary Table


As we can see from the summary table and graphs (Figure 15 and Figure 16 respectively), Test 1 yielded the highest memory and CPU usage while our baseline, Test 5, which uses no animations and no physics scripts, yielded the lowest, as expected. The only unexpected result was that passive ragdolls, also called as traditional ragdolls, yielded higher hardware usage values compared to active ragdolls without animations. Further looking into it, it can be assessed that it is due to the number of collisions increasing as a result of a lack of spring values and more physics calculations necessary to be made.



![image](https://github.com/user-attachments/assets/079cbafb-66de-42b4-b231-7e32e970e4a1)    
Figure 16: Performance comparison graphs


As a closing note, while the usage of active ragdolls is computationally intensive, I believe it is worth the performance loss with the achieved result. Implementation of this mechanic can open up new possibilities in many genres ,ranging from immersive simulations to casual games, where chaotic interactions add to the fun factor.
