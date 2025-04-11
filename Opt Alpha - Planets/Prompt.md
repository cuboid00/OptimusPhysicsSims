
Goal: Generate a single, self-contained HTML file that uses Three.js (v0.163.0 or later via CDN and importmap) to create an interactive 3D simulation of the inner and outer planets of our solar system orbiting a central Sun.

Core Requirements:

HTML Structure: Create a basic HTML page with a <canvas> element for the 3D scene, a <div> for status messages (#info), and a <div> for UI controls (#control-panel).

CSS Styling: Include CSS within <style> tags to:

Make the canvas fill the viewport.

Set a dark background.

Style the #info div (absolute position, centered text).

Style the #control-panel div (absolute position top-left, dark semi-transparent background, padding, basic styling for labels, sliders, checkboxes, and value displays).

Style planet labels (.label class for CSS2DObject).

JavaScript Logic (using ES Modules and importmap):

Setup: Initialize a Three.js scene, perspective camera, WebGL renderer, CSS2DRenderer (for labels), and OrbitControls.

Starfield: Create a static starfield background using THREE.Points distributed spherically.

Sun: Create a central Sun object:

Use a SphereGeometry.

Make it emissive (yellow/orange).

Optionally include a placeholder texture URL (e.g., from placehold.co).

Add a slightly larger, emissive wireframe mesh overlaying the main Sun sphere.

Planets:

Include data (name, distance [AU], orbital period [days], eccentricity, inclination [deg], diameter [km], color hint, mass [relative to Earth]) for Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune, and Pluto (as a dwarf planet).

For each planet:

Create a SphereGeometry scaled appropriately (use a consistent scaling factor for radii based on diameter, ensuring visibility).

Use an emissive MeshStandardMaterial based on the planet's color hint.

Implement elliptical orbits based on semi-major axis (derived from distance), eccentricity, and inclination. Use Kepler's equation (or a reasonable approximation) to calculate position over time. Apply inclination correctly. Place orbits relative to the Sun (focus).

Create a visual representation of the orbit path (e.g., LineLoop or LineDashedMaterial) associated with each planet.

Add CSS2DObject labels displaying the planet's name, positioned near the planet.

Specifically for Saturn: Add a simple ring system using RingGeometry.

Gravity Spheres:

For each planet, create a semi-transparent, wireframe SphereGeometry (MeshBasicMaterial is fine).

Center this sphere on the planet's current world position in each frame.

Scale the radius of this sphere based logarithmically on the planet's mass (e.g., base_radius + log10(mass + 1) * scale_factor). Make these spheres visually distinct from the planets themselves (e.g., white or grey wireframe).

Earth-Mars Line:

Create a Line object connecting the current world positions of Earth and Mars.

Update the line's vertices in each frame.

Implement logic to change the line's color based on the approximate Hohmann transfer window alignment: calculate the relative angle between Earth and Mars in the orbital plane; if the angle is within a defined window (e.g., Mars leading Earth by ~44° +/- 20°), color the line green, otherwise color it red.

Animation: Use requestAnimationFrame and THREE.Clock to update planet positions, gravity sphere positions, the Earth-Mars line, and render the scene.

Controls (#control-panel):

Sliders:

Sun Wireframe Brightness (emissiveIntensity): Controls the emissive intensity of the Sun's wireframe overlay.

Animation Speed: Multiplies the time delta used for orbital calculations.

Planet Brightness (emissiveIntensity): Controls the emissive intensity of all planets simultaneously.

Checkboxes:

Show Orbits: Toggles the visibility of all planet orbit lines.

Show Labels: Toggles the visibility of all planet CSS2DObject labels.

Show Gravity Spheres: Toggles the visibility of the wireframe gravity spheres.

Show Earth-Mars Line: Toggles the visibility of the line connecting Earth and Mars.

UI Updates: Ensure sliders display their current numeric value next to them, updating on change. Checkboxes should reflect the initial state and update the scene accordingly.

Post-processing: Implement a simple bloom effect using EffectComposer, RenderPass, UnrealBloomPass, and OutputPass.

Window Resizing: Handle window resize events to update camera aspect ratio and renderer/composer sizes.

Performance: Use reusable THREE.Vector3 objects where appropriate for position calculations/updates.

Output: A single HTML file (.html) containing all the necessary HTML, CSS, and JavaScript code. The simulation should start automatically upon opening the file in a modern web browser. Use CDN links for Three.js and its addons within the importmap.
