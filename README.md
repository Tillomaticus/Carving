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

Mesh deformation
<div style="text-align:center;">
   <img src="https://github.com/user-attachments/assets/596636fe-a48c-4edb-8652-bb33acb59b1c" alt="alt text" width="300"/>
</div>

Knife carving
<div style="text-align:center;">
   <img src="https://github.com/user-attachments/assets/e81c5e0e-9e4d-4e39-b543-8dda9efb32dd" alt="alt text" width="300"/>
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

### Performance
With on-runtime mesh deformation and regeneration, performance can quickly become an issue. While I have taken some precautions, by limiting the amount of times the carving and thus mesh deformation can occur, I have yet to find some performance issues. 
Performance may become an issue in the future though, once i tune up the mesh resolution, increasing the number of vertices. So I will need to keep a close eye on the FPS and especially CPU load. 
There are some improvements to be made, especially regarding the raycasting for both aligning the knife tip with the deformed mesh, as well with the one responsible for finding the correct face to deform. If I eliminate the need for raycast and instead achieve the same effect mathematically, I would be able to remove the Mesh Collider, reducing some recalulation costs here aswell. 
But since the performance currently is keeping up, I will focus on other tasks first.



## 🚀 Whats next? 
- Creating a goal: Having a template that you have to match, like carving a vase or something like that.
- Shading issues with the dynamic mesh
- Experiment with higher mesh resolution
- Polishing (Especially knife animation & jumpiness while carving)
- UI
- Visuals
- Different materials to choose from (metal, stone, ice, wood)
- Performance optimizations (if necessary)




