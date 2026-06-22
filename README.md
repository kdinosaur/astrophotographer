An imagined portfolio page for an astrophotographer or space & stars enthusiast. 
Uses Three.js, SphereGeometry, and THREE.Points to generate a universe of stars. 
Uses mouse parallax to grab the user's raw motions.

More details

1. Nebula Background
Instead of using a static space background image, the code generates a moving nebula using Fractal Brownian Motion (FBM) and noise algorithms inside a fragment shader. 

2. Diffraction Spikes for stars
A custom star fragment shader mathematically draws star effects on each particle to create the glow

3. Twinkling Star Math
Most basic space animations use simple sine waves for twinkling, which looks robotic. This code uses flash=pow(sin(t),10.0) for the vertex shader.
The stars stay at a low simmer for a while and then suddenly "flash" or pulse rapidly which I think looks more realistic to how the stars look due to the atmosphere.

4. Interactive Parallax & Orbiting
The universe responds to the user in two ways simultaneously:
-Passive & Active Orbit: The OrbitControls plugin slowly auto-rotates the camera, but users can click and drag to orbit through the 3D starfield themselves.
-Mouse Parallax: The code captures the raw coordinates of your mouse pointer (mouseX/mouseY) and applies tilting effect to the entire universe group

5. The Three.js Universe
The Nebula Sphere: The code creates a huge SphereGeometry with a radius of 1000 units. It sets side: THREE.BackSide, which means the texture is rendered on the inside of the sphere. The camera sits center, looking out at the walls of this sphere.
The Star Field: Instead of creating 2,500 individual 3D objects (which would crash the browser), it uses THREE.Points. This tells the GPU to render 2,500 coordinates as single vertex particles in a single draw call, making it appear smooth.

6. The GLSL Shaders  
Shaders are programs written in GLSL (OpenGL Shading Language) that run directly on your graphics card.
Vertex Shaders: Handles where things are. The star vertex shader takes the 3D coordinates, applies the camera angle, scales the star size based on how close it is to the camera, and calculates how brightly it should twinkle.
Fragment Shaders: Handles what color the pixels are. The nebula fragment shader blends dark blues, purples, and gold texturing seamlessly across the screen based on mathematical noise, while the star fragment shader calculates the flare transparency for each star

Inspired by: https://www.jesuisundev.com/en/i-built-the-entire-universe-in-javascript/

