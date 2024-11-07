<template>
    <div ref="canvasContainer" class="canvas-container"></div>
  </template>
  
  <script setup lang="ts">
  import { onMounted, ref, onBeforeUnmount } from 'vue';
  import * as THREE from 'three';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader'; // Import GLTFLoader
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'; // Import OrbitControls
  
  const canvasContainer = ref(null);
  
  const initThreeJS = () => {
    // Create a scene
    const scene = new THREE.Scene();
    
    // Create a camera
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 0, 5); // Set camera position
    
    // Create a renderer
    const renderer = new THREE.WebGLRenderer({ alpha: true }); // Enable transparency
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setClearColor(0x000000, 0); // Set background to transparent
    
    // Append the renderer to the canvas container
    canvasContainer.value.appendChild(renderer.domElement);
    
    // Load the GLTF model
    const loader = new GLTFLoader();
    let model; // Reference to the loaded model
    
    loader.load('/img/me.glb', (gltf) => {
      model = gltf.scene;
      
      // Center the model
      model.position.set(0, -1.5, 3); // Position the model near the center of the canvas
      scene.add(model);
    }, undefined, (error) => {
      console.error('An error occurred while loading the model', error);
    });
    
    // Add ambient light
    const ambientLight = new THREE.AmbientLight(0xffffff, 1); // Soft white light
    scene.add(ambientLight);
    
    // Add directional light
    const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
    directionalLight.position.set(5, 5, 5);
    scene.add(directionalLight);
    
    // Setup OrbitControls for user rotation
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableZoom = true; // Allow zoom if desired
    controls.enablePan = true; // Allow panning if desired
    controls.target.set(0, -1, 3); // Set the target point to the model's position
    controls.update(); // Update controls to take effect
    
    // Handle window resizing
    const onWindowResize = () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    };
    
    // Animation loop
    const animate = () => {
      requestAnimationFrame(animate);
      controls.update(); // Update controls
      renderer.render(scene, camera);
    };
  
    animate();
    
    // Listen to window resize
    window.addEventListener('resize', onWindowResize);
    
    // Cleanup on component unmount
    onBeforeUnmount(() => {
      window.removeEventListener('resize', onWindowResize);
      renderer.dispose(); // Dispose of the renderer
      if (model) {
        model.traverse((child) => {
          if (child.isMesh) child.geometry.dispose(); // Dispose of model geometry
        });
      }
    });
  };
  
  // Initialize Three.js when component is mounted
  onMounted(() => {
    initThreeJS();
  });
  </script>
  
  <style scoped>
  .canvas-container {
    position: relative;
    width: 100vw; /* Full width */
    height: 100vh; /* Full height */
  }
  </style>
  