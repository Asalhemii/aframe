<html>
  <head>
    <meta charset="utf-8" />
    <title>Stressor Wyrm in A-Frame</title>
    <script src="https://aframe.io/releases/1.4.2/aframe.min.js"></script>
  </head>
  <body>
    <a-scene background="color: #101010">
      <!-- Lighting -->
      <a-entity light="type: point; intensity: 1.5; distance: 15; color: #ff0077" position="2 4 4"></a-entity>
      <a-entity light="type: ambient; intensity: 0.5; color: #666"></a-entity>

      <!-- Camera -->
      <a-entity position="0 1.6 6">
        <a-camera></a-camera>
      </a-entity>

      <!-- Creature: Stressor Wyrm -->
      <a-entity id="stressorWyrm" position="0 1.5 -3" animation__hover="property: position; dir: alternate; dur: 2000; easing: easeInOutSine; loop: true; to: 0 2 -3">
        <!-- Body -->
        <a-sphere radius="1" color="#2244ff" id="wyrmBody"
                  animation__pulse="property: scale; dir: alternate; dur: 1000; easing: easeInOutSine; loop: true; to: 1.2 1.2 1.2">
        </a-sphere>
        <!-- Eyes -->
        <a-sphere position="-0.3 0.3 0.9" radius="0.1" color="#ff0000"></a-sphere>
        <a-sphere position="0.3 0.3 0.9" radius="0.1" color="#ff0000"></a-sphere>
        <!-- Tentacles (stress react) -->
        <a-cylinder position="-0.6 -0.6 0" height="1.2" radius="0.05" color="#ff55aa" rotation="0 0 45"></a-cylinder>
        <a-cylinder position="0.6 -0.6 0" height="1.2" radius="0.05" color="#ff55aa" rotation="0 0 -45"></a-cylinder>
      </a-entity>

      <!-- Sky -->
      <a-sky color="#000015"></a-sky>
    </a-scene>

    <script>
      let stressLevel = 0; // Simulated stress value from 0 to 1
      const body = document.getElementById('wyrmBody');

      function simulateStress() {
        stressLevel = (Math.sin(Date.now() / 1000) + 1) / 2; // oscillates between 0 and 1

        // Color shifts from blue to red based on stress
        const r = Math.floor(34 + stressLevel * (255 - 34));
        const g = Math.floor(68 - stressLevel * 68);
        const b = Math.floor(255 - stressLevel * 200);
        body.setAttribute('color', `rgb(${r},${g},${b})`);

        // Scale pulsates more intensely with stress
        const scaleFactor = 1 + stressLevel * 0.5;
        body.setAttribute('scale', `${scaleFactor} ${scaleFactor} ${scaleFactor}`);

        requestAnimationFrame(simulateStress);
      }

      simulateStress();
    </script>
  </body>
</html>
