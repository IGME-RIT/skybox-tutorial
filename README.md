# Skybox Tutorial

This example uses the code established in the obj loading example to demonstrate rendering a skybox.

# About

This example uses the code established in the obj loading example to demonstrate rendering a skybox. There is actually very little new code for rendering the skybox. The texture for the box is loaded with SOIL, an inverted cube with carefully adjusted UV coordinates are imported from Maya and loaded with the obj loader already present. The texture is rendered to the cube and the cube is translated to the location of the camera. A self-lit shader has to be used for the skybox since lighting doesn't really work with it. Finally, we make use of the layer system previously established to put the skybox on a separate layer to render it without affecting the depth buffer.

There are 5 static component classes that make up the base functionality for this example:

1) RenderManager
	- This class maintains the display list for the scene being rendered and thus handles the processes of updating and drawing all of the RenderObjects that have been instantiated in the scene.

2) CameraManager
	- This class maintains data relating to the view and projection matrices used in the rendering pipeline. It also handles updating this data based on user input.

3) InputManager
	- This class maintains data for the current state of user input for the mouse and keyboard.

4) LightingManager
	- This class maintains data for an array of eight lights, each possessing a transform, color and power, handles the updating thereof and maintains GPU-side buffers reflecting this data for use in the shaders.

5) ResourceManager
	- This class maintains all the data from external sources necessary to run the program. In this instance, this includes obj loading, parsing, and storage, VAO, VBO, and EBO generation and storage, shader loading, compiling and linking, and uniform buffer object generation, binding and storage.

RenderObject
	- Tracks the instance of an object that can be drawn to the screen. Contains data for transforms, a mesh, a shader, drawing mode (eg triangles, lines), and a layer. The layer is a value that can be used to mask certain objects from a draw call. The object has a layer which is some power of 2 and then there is a mask for the draw call which is a 32-bit number. A bit-wise & between these numbers decides whether or not the object in question is drawn.

SHADERS
  - Now use uniform buffer objects for receiving uniform data.

vShader.glsl
  - Through shader, nothing fancy

fShader.glsl
  - Applies a Phong-lighting model based on the data sent from the lighting manager, functions the same as the Phong shader from the geometric lighting improved example.

# Setup

In order to setup, run the following in a shell, then open the project in your preferred editor. Windows setup has been configured for use with Visual Studio.

Windows:
```
cd path/to/folder
setup.cmd
```
Linux:
```
cd path/to/folder
./setup
```
