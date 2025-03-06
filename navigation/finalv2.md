--- 
comments: true
layout: page
title: CSSE1 Final Exam
description: Final exam for CSSE1
author: Ruhaan Bansal
permalink: /csse1finalv2/
---
## Final Exam CSSE 1 

### Solo Review 
#### For the three tinkers I made on the adventure game I will be showing one in particular detail.

#### The tinker is the class collision in which I layered the collision block over the rock in the background so that the player can't go forward or move ahead without answering the questions.

#### To make sure that the collision is layered over the rock and provides the player questions I created a file called collision.js. The code file is underneath

<img width="640" alt="Image" src="https://github.com/user-attachments/assets/0f36b61e-724e-49e2-b088-e0d07b7864d9" />
<img width="640" alt="Image" src="https://github.com/user-attachments/assets/2866f4fe-1d84-48fe-8f27-7981ffba5de7" />
<img width="640" alt="Image" src="https://github.com/user-attachments/assets/02a9889d-8c63-4bae-89c9-35ded3bc70b4" />

#### Then I implented the format of the collision to the new collision with an blank transparent image of 128 px x 128 px. The code for the collision is here:

<img width="640" alt="Image" src="https://github.com/user-attachments/assets/d004df26-e336-413f-8e71-f93e2c7eb09d" />

##### I also had to import:
import Collision from './Collision.js'; 

##### I also had to export:
{ class: Collision, data: sprite_data_collision}

### It may seem like the collision is exactly the same as an NPC but there are some differences such collision's hitbox increased and the area of the collision that the blank image captures is way more than the regular NPC.