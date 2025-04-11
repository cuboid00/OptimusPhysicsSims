Benchmark Prompt:

Objective: Generate a single, self-contained HTML file that uses Three.js (version 0.163.0 or later) to create a 3D visualization simulating the concept of spacetime curvature due to mass, inspired by General Relativity.

Core Requirements:

    HTML Structure: Create a standard HTML5 document (<!DOCTYPE html>).

    Three.js Setup:

        Include Three.js using an importmap pointing to https://unpkg.com/three@0.163.0/ (or a compatible version).

        Set up a basic Three.js scene, perspective camera, and WebGL renderer.

        Add OrbitControls for camera manipulation, imported from three/addons/.

        Implement a standard requestAnimationFrame loop for animation.

        Include basic lighting (e.g., AmbientLight, PointLight).

        Ensure the canvas fills the viewport and handles window resizing.

    Scene Objects:

        Spacetime Grid: Create a PlaneGeometry with a significant number of segments (e.g., 50x50 or more) displayed as a wireframe (e.g., green color). Position it horizontally (like a floor).

        Central Mass: Create a SphereGeometry representing a central, massive object (e.g., a yellow "star"). Position it near the center of the plane. Make it slightly emissive if possible.

        Orbiting Mass: Create a smaller SphereGeometry representing an orbiting object (e.g., a blue "planet").

    Animation & Interaction:

        Animate the smaller sphere to orbit the central sphere in a circular path roughly parallel to the plane.

        Crucially: Implement dynamic deformation of the PlaneGeometry vertices.

            The vertical position (y coordinate after the plane is rotated horizontally) of each vertex on the plane should be pushed downwards based on its proximity to both the central mass and the orbiting mass.

            The deformation effect should simulate a "gravity well," being strongest near each mass and diminishing with distance (e.g., using an inverse distance or inverse square distance relationship, potentially with a falloff exponent).

            The influence of both masses should be combined (e.g., additive).

            The geometry's position attribute needsUpdate flag must be set to true each frame after modification.

    Code Style:

        Use modern JavaScript (ES Modules) within <script type="module">.

        Use clear variable names.

        Define configuration constants (like object sizes, orbit radius, deformation strength, segment count) near the top for easy adjustment.

Output: A single HTML file containing all necessary HTML, CSS (minimal, for body/canvas styling), and JavaScript code to run the described simulation directly in a browser supporting ES Modules and WebGL.
