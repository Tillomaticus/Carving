# Carving
## Sneak preview of a small Unity based Mobile Game
Code is on Unity Version Control (VCS, formerly PlasticSCM), as that aligns with my workflow better. I probably will upload it here, once i reach a solid version.

## 🎯Inspiration
A small hobby project to create a mobile game with Unity to improve my skills with the constraints of mobile development, like small screen and playarea as well as limited performance. 
I went with a very minimal idea, something that focuses more on technical aspects, as i am not a great artist.

## 🕹️ What it does
You have a rotating stone in the middle, touch to slide the knife and start carving off the edges. Slide your finger on the side to move the knife vertically to carve on different heights.

Screenshots from the Game View
<div style="text-align:center;">
   <img src="https://github.com/Tillomaticus/Carving/blob/main/Carving.gif" alt="alt text" width="300"/>
</div>

Mesh deformation (with broken shading)
<div style="text-align:center;">
   <img src="https://github.com/user-attachments/assets/596636fe-a48c-4edb-8652-bb33acb59b1c" alt="alt text" width="300"/>
</div>

Knife carving (with fixed shading)
<div style="text-align:center;">
   <img src="https://github.com/user-attachments/assets/158a0453-cf15-499c-9e32-f200c1c0343b" alt="alt text" width="300"/>
</div>

## 🛠️ How its build
- Unity3D (6.0)
- Visual Studio Code
- ChatGPT (for assistance with the Mesh deformation)

## 🚧 Challenges

### Mesh Generation and Deformation
In order to achieve the mesh carving visual effect. I first had to generate a mesh, then i had to find the face i want to move, then move it inwards and finally regenerate the mesh and collider. 
The mesh generation is done at startup. Once we start carving, I have to find out which face is touched by the knife and then move it inward, so it looks as if the knife has scraped material off. 
To find the correct face I cast a ray from the knife tip towards the radial center of the cylinder. I then take the hit point and translate it into object space. I then find the face that is the closest to my hitpoint. Afterwards i get the vertices of that face and move inwards towards the radial center, deforming the mesh. At last I have to regenerate the mesh aswell as the mesh collider. 
I do need to utiilize a mesh collider here to make the raycast work. 


### Mesh Shading
When generating the mesh at runtime I run into an issue with shading. When creating a continous mesh, as it was needed for the deformation, the edges are soft edges. This means the edges will appear somewhat soft aswell. 
But for the edge at the top cap, I need a hard edge for the shading to look realistic. 
To create a hard edge at runtime in Unity, you need to cut the mesh, and with it duplicating the vertices of the edge. So that you basically have two vertices at the same position, each belonging to one of the overlapping edges.
However this would also mean, that when wanting to move a side face inside, as I am just finding the vertices of that face, as they are not connected anymore. 
And with that I would leave the vertices of the overlapping edge untouched. 
As a solution I created a dictionary for all vertices. When generating the Mesh, i would then check the dictionary if there was already a different vertex at that position and if yes, adding the current vertex as a shared Vertex.
Now whenever I move a vertex, i can simply check if there are any shared Vertices and then move them aswell. This way I can keep the behaviour of a continous mesh, while its actually not continous but has cuts for the hard edges.
The difference in shading can be seen in the screenshots above.

### Performance
With on-runtime mesh deformation and regeneration, performance can quickly become an issue. While I have taken some precautions, by limiting the amount of times the carving and thus mesh deformation can occur, I have yet to find some performance issues. 
Performance may become an issue in the future though, once i tune up the mesh resolution, increasing the number of vertices. So I will need to keep a close eye on the FPS and especially CPU load. 
There are some improvements to be made, especially regarding the raycasting for both aligning the knife tip with the deformed mesh, as well with the one responsible for finding the correct face to deform. If I eliminate the need for raycast and instead achieve the same effect mathematically, I would be able to remove the Mesh Collider, reducing some recalulation costs here aswell. 
But since the performance currently is keeping up, I will focus on other tasks first.


## 📖 Learnings
- Its a bad idea to have your game elements on the right edge of the screen, when using portrait mode, as most people are right handed, and their thumb will hide them.
- Manually generating UV layouts without visual representation is tough.
  

## 🚀 Whats next? 
- Creating a goal: Having a template that you have to match, like carving a vase or something like that.
- Experiment with higher mesh resolution
- better UI
- Visuals
- Sound
- Performance optimizations (if necessary)
- Improve UV Layout for better texturing

## 🏁 Done
- Shading issues with the dynamic mesh ✔️
- Different materials to choose from (metal, stone, ice, wood) ✔️
- Polishing (Especially knife animation & jumpiness while carving) ✔️
- Ability to switch the knife from right side to left side ✔️
- Simple UI ✔️
  



