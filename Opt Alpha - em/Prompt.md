Objective: Generate a complete, single HTML file that uses Three.js (via ES Modules and CDN importmap) to create an interactive 3D visualization simulating the magnetic field of a solenoid, approximated as a magnetic dipole.

Core Requirements:

    HTML Structure:

        Standard HTML5 document (<!DOCTYPE html>).

        head section with meta charset="UTF-8", meta viewport, and a relevant title.

        Inline <style> block for basic CSS: black background, hide body overflow, style a simple overlay info text.

        body containing a placeholder for the Three.js canvas and an absolutely positioned div (e.g., #info) for displaying descriptive text about the simulation.

        An importmap script block correctly mapping "three" and "three/addons/" to their respective ES Module CDN URLs (use a recent version like 0.163.0 or later).

        A <script type="module"> block containing all the JavaScript logic.

    Three.js Scene Setup:

        Initialize a THREE.Scene, THREE.PerspectiveCamera, and THREE.WebGLRenderer.

        Set the renderer size to match the window and append its domElement to the body.

        Add basic lighting (e.g., AmbientLight and DirectionalLight).

        Implement OrbitControls for user interaction (orbit, zoom, pan). Enable damping for smoother interaction.

    Solenoid Representation:

        Create a 3D mesh representing a solenoid (coil of wire).

        Use THREE.TubeGeometry based on a custom THREE.Curve class that defines a helix path (parameterized by radius, height, and number of turns).

        Apply a THREE.MeshStandardMaterial to the solenoid mesh, giving it a metallic appearance (e.g., copper color, appropriate metalness/roughness).

        Bonus: Create and apply an emissive texture map to the solenoid material. Animate the texture's UV offset (texture.offset.x) in the animation loop to simulate the flow of current.

    Magnetic Field Visualization:

        Use THREE.Points to represent the magnetic field lines with a large number of particles (e.g., 2000+).

        Apply a THREE.PointsMaterial:

            Use a custom particle texture (generated via Canvas API or loaded) that looks like a soft, glowing dot (e.g., radial gradient).

            Set an appropriate particle size and color (e.g., blue/light blue).

            Use AdditiveBlending and disable depthWrite for a better glow effect.

            Ensure sizeAttenuation is enabled.

        Initialize particle positions randomly within a defined volume around the solenoid.

    Physics Simulation (Magnetic Dipole Approximation):

        Define constants for simulation parameters (coil dimensions, particle count, animation speed, dipole strength factor, reset distance).

        Implement a JavaScript function magneticDipoleField(position, dipoleMoment, targetVector) that calculates the approximate magnetic field vector B at a given position based on the dipole formula: B(r) ∝ (3 * (m · r) * r / |r|^5) - (m / |r|^3). Assume the dipole moment vector m is aligned with the Z-axis. Ignore the mu0 / 4pi constant, as only the direction and relative magnitude matter for visualization. Handle potential division-by-zero near the origin.

        Inside/Outside Logic: In the particle animation, check if a particle is approximately inside the cylindrical volume of the solenoid.

            If inside, approximate the field as uniform and pointing purely along the solenoid's axis (e.g., +Z).

            If outside, use the magneticDipoleField function to get the field direction.

        Particle Movement: In the animation loop (requestAnimationFrame), iterate through each particle. Get the magnetic field direction vector at the particle's current position (using the inside/outside logic). Normalize the field vector and update the particle's position by moving it along this direction, scaled by deltaTime and fieldAnimationSpeed.

        Particle Reset: Implement logic to reset a particle's position (e.g., randomly near one end of the solenoid or within a specific starting volume) if it travels beyond a certain resetDistance from the origin or gets too close to the origin/poles (to avoid visual artifacts or extreme speeds).

    Visual Enhancements (Post-processing):

        Implement post-processing using EffectComposer.

        Add a RenderPass and an UnrealBloomPass to create a glow effect for the emissive solenoid and the field particles. Tune the bloom parameters (strength, radius, threshold) for a pleasing effect.

    Animation Loop & Event Handling:

        Use requestAnimationFrame for the main animation loop.

        Use THREE.Clock to get deltaTime for smooth, frame-rate-independent animation. Consider clamping deltaTime to prevent large jumps.

        Update OrbitControls in the loop.

        Render the scene via the EffectComposer.

        Include a window.onresize event listener to update the camera aspect ratio, renderer size, and composer size.

Expected Output: A single, runnable HTML file that displays an interactive 3D visualization of a glowing solenoid surrounded by flowing particles representing its magnetic field, with camera controls and a bloom effect, closely matching the described functionality. The code should be reasonably well-structured and use modern JavaScript features within the module script.
