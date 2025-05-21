## OpenGL Rendering Engine (Learning Project)

### Overview

This project was my first dive into OpenGL. I built a simple rendering pipeline that progressed from drawing basic shapes to displaying fully lit and textured 3D models. While it's not a full "engine," it helped me get familiar with the core components of real-time rendering. I've been exposed to computer visualization concepts before (more on that later), so this was a really fun project to actually put all my learning to good use. This project also branched into another side project intended solely for 3D models (made from Blender).

**Tech stack**: `C++` `OpenGL` `GLSL`

---

### 1. Primitive Shapes and Buffers

I started with rendering simple primitives: a triangle, then a square, and finally a cube. This helped me get a handle on OpenGL's VAO, VBO, and EBO system. It's also where I wrote my first Vertex and Fragment shaders for OpenGL. I had written shaders before (HLSL) inside Unity's scriptable pipeline, and GLSL is mostly the same, but nonetheless it was really fun seeing how customizable you can get with no limiting factor like Unity. I also got to apply some cool math in this portion, where I manipulated my objects with rotation equations using transformation matrices, which I learned from a Graphics Book by Fletcher Dunn.

![My first triangle rendered using a VAO.](css/images/opengl-triangle.png)  
*My first triangle rendered using a VAO.*

![A rotating cube, textured with an image of my friend's face.](css/images/opengl-cube.png)  
*A rotating cube, textured with an image of my friend's face.*

https://github.com/user-attachments/assets/944889cc-bb44-40c2-a25e-2117f51b66d9
*Multiple rotating cubes, textured with an image of my friend's face!*

---

### 2. Camera System

Next, I added a camera system with basic movement + zoom controls. This made navigating the scene possible and laid the groundwork for interacting with 3D space. It was cool seeing how OpenGL has so much support for Input mapping, which was something I was not expecting going into this project.

https://github.com/user-attachments/assets/30b52ccd-67e0-4879-b19f-83323796b024
*Input mapped camera system. (in a more complex scene)*

---

### 3. Textures

Once I had geometry and movement in place, I added texture support. This included loading images, mapping TextureCoords correctly, and testing with multiple textured cubes. I messed around with a new library `stb_image` by Sean Barret. And I learned about Mipmaps and Texture Filtering. I also got to do more work with shaders here, as now I could use the TextureCoords in the color processing.

![Normal mapped image](css/images/opengl-normalimage.png)  
*Totally normal image of my friend, that definitely doesn't have LeBron secretly hidden as an opaque second texture.*

![Light mapping](css/images/opengl-specularmap.png)  
*Textured cube, with light mapping.*

---

### 4. Lighting

This was by far my favourite part of the project, which is probably reflected by just how long this text is. I learned a ton about all the many ways lighting can influence an object. Pretty soon after I implemented a basic Phong lighting model, which I learned all about ambient, diffuse, and specular lights. This was a massive highlight for me, as I am obsessed with math, and the calculations required for these lights are so intriguing and intuitive, I could write a whole essay about how much I loved the math behind these techniques, but I'll save you the time.

I spent a ton of time messing around with different values to simulate different materials, which can be found [here](http://devernay.free.fr/cours/opengl/materials.html). After that worked, I added lighting maps (Diffuse, and Specular) to my textures. This really opened my eyes to what’s possible with materials. I then extended the project to support directional light, point lights, and spotlights—all active in one scene.

![Directional light](css/images/light_casters_directional.png)  
*Directional light diagram, showing how all rays are parallel, meaning light calculation is the same for all rays.*

![Point light](css/images/light_casters_point.png)  
*Point light diagram, showing that as light scatters from its source, it becomes attenuated.*

![Spotlight](css/images/light_casters_spotlight_angles.png)  
*Spotlight diagram, showing the vector pointing from the fragment to the light, the radius (Phi ϕ), and the dot product of the light direction and the spotlight direction (Theta θ).*

---

### 5. Model Loading with Assimp

I integrated another library: `Assimp` to load external 3D models. This allowed me to render more complex assets with their own defined vertices, faces, meshes and materials. This part was actually pretty straightforward for me, as I had already built up a lot of foundations in the project beforehand. It did involve me making two new classes. I even got to add some pretty advanced stuff in here like tangent-space normal mapping and vertex skinning, but I never got to utilize them.

![Assimp model](css/images/opengl-assimp.png)  
*Simplistic model of Assimp's structure.*

---

### 6. Depth and Stencil Testing

Here I experimented around with depth and stencil testing inside my project. I learned about linear/non-linear depth buffers to calculate depth value precision, and how the depth value is more precise the closer it is to the near plane. I also had fun with some heavy math operations, as calculating the depth values involved a ton of work with the projection matrix, which I learned from this [article](https://www.songho.ca/opengl/gl_projectionmatrix.html).

Afterwards I played around with Stencil Testing, which I felt was super valuable experience. There is a bunch of functions already baked in to OpenGL's library, so I had a ton of settings to explore. I ended up using the stencil buffer to outline various objects within my scene. I made an X-ray, and a "selection" action (like selecting something in a RTS) inside an outlining algorithm.

![Projection matrix](css/images/opengl-viewspace.png)  
*Near and Far plane of the projection matrix, used in depth value calculations.*

![Nonlinear depth](css/images/opengl-nonlineargraph.png)  
*Non-linear graph of the relation between the z-value and the resulting depth buffer's value.*

---

### Learning Process

Even though this was my first OpenGL project, I had a solid foundation going in. I'd already read _3D Math Primer for Graphics and Game Development_ (Fletcher Dunn) and _Foundations of Game Engine Development_ by Eric Lengyel, as well as a strong theoretical understanding of linear algebra from Gilbert Strang's textbooks. Those books helped a lot with the math side of things.

Throughout the project, I followed the LearnOpenGL tutorials. Thanks to the reading I'd done beforehand, the material clicked pretty quickly, and I was able to apply it in my own setup without just copying the code.

---

### Source Code & GitHub History

All the code for this project is available on my GitHub repository, including the full source, shaders, and supporting assets. You can actually follow along with how I built each part of the renderer from the ground up, step by step by checking out the Commit Graph. It's a pretty honest snapshot of how I approached the project and how it evolved over time.
