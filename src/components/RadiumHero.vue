<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import * as THREE from 'three';

const container = ref(null);
let scene, camera, renderer, animationFrame;
let workspaceGroup;
let headGroup, leftArm, rightArm;

const init = () => {
  if (!container.value) return;

  // --- Scene Setup ---
  scene = new THREE.Scene();
  
  const aspect = container.value.clientWidth / container.value.clientHeight;
  camera = new THREE.PerspectiveCamera(45, aspect, 0.1, 10000);
  camera.position.set(13, 11, 13);
  camera.lookAt(0, 0, 0);

  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.setSize(container.value.clientWidth, container.value.clientHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  container.value.appendChild(renderer.domElement);

  workspaceGroup = new THREE.Group();
  scene.add(workspaceGroup);

  // --- Materials ---
  const darkMat = new THREE.MeshStandardMaterial({ color: 0x0a0a0a, roughness: 0.1 });
  const neonPurpleMat = new THREE.MeshStandardMaterial({ color: 0x9d4edd, emissive: 0x9d4edd, emissiveIntensity: 2.5 });
  const neonYellowMat = new THREE.MeshStandardMaterial({ color: 0xffd000, emissive: 0xffd000, emissiveIntensity: 4 });
  const neonCyanMat = new THREE.MeshStandardMaterial({ color: 0x00f5ff, emissive: 0x00f5ff, emissiveIntensity: 3 });
  const deskMat = new THREE.MeshStandardMaterial({ color: 0x121212, roughness: 0.2 });
  const skinMat = new THREE.MeshStandardMaterial({ color: 0x333333, roughness: 0.1 }); // Glossy plastic-like
  const clothMat = new THREE.MeshStandardMaterial({ color: 0x240046, roughness: 0.5 }); // Purple Hoodie
  const screenMat = new THREE.MeshStandardMaterial({ color: 0x111111, emissive: 0x3c096c, emissiveIntensity: 1.5 });

  // 1. Desk
  const desk = new THREE.Mesh(new THREE.BoxGeometry(9, 0.3, 5), deskMat);
  desk.position.y = -1;
  workspaceGroup.add(desk);

  // 2. Laptop & Screen Code
  const laptopGroup = new THREE.Group();
  laptopGroup.position.set(0, -0.7, 0);
  workspaceGroup.add(laptopGroup);

  const laptopBase = new THREE.Mesh(new THREE.BoxGeometry(3.6, 0.15, 2.6), darkMat);
  laptopGroup.add(laptopBase);

  const laptopScreen = new THREE.Mesh(new THREE.BoxGeometry(3.6, 2.6, 0.1), screenMat);
  laptopScreen.position.set(0, 1.3, -1.3);
  laptopScreen.rotation.x = -Math.PI * 0.03;
  laptopGroup.add(laptopScreen);

  // Keyboard (On Laptop Base)
  const keyboardGroup = new THREE.Group();
  keyboardGroup.position.set(-1.4, 0.1, 0.2);
  laptopGroup.add(keyboardGroup);

  const keyGeom = new THREE.BoxGeometry(0.2, 0.05, 0.2);
  const keyMat = new THREE.MeshStandardMaterial({ color: 0x1a1a1a });
  for (let row = 0; row < 4; row++) {
    for (let col = 0; col < 12; col++) {
      const key = new THREE.Mesh(keyGeom, keyMat);
      key.position.set(col * 0.25, 0, row * 0.25);
      keyboardGroup.add(key);
    }
  }

  // Mouse (On Desk)
  const mouseGroup = new THREE.Group();
  mouseGroup.position.set(3, -0.85, 1.5);
  workspaceGroup.add(mouseGroup);

  const mouseBody = new THREE.Mesh(
    new THREE.SphereGeometry(0.25, 16, 16),
    new THREE.MeshStandardMaterial({ color: 0x1a1a1a, roughness: 0.3 })
  );
  mouseBody.scale.set(1, 0.6, 1.4);
  mouseGroup.add(mouseBody);

  const mouseLight = new THREE.PointLight(0x9d4edd, 2, 2);
  mouseLight.position.y = 0.2;
  mouseGroup.add(mouseLight);


  // Simulated Code Lines
  const codeLinesGroup = new THREE.Group();
  codeLinesGroup.position.set(-1.5, 0.9, 0.06); 
  laptopScreen.add(codeLinesGroup);

  let codeLines = [];
  const linePaints = [0x00f5ff, 0x9d4edd, 0xffffff];

  const createCodeLine = (index) => {
    const lineWidth = Math.random() * 1.6 + 0.5;
    const line = new THREE.Mesh(
      new THREE.PlaneGeometry(lineWidth, 0.08),
      new THREE.MeshStandardMaterial({ 
        color: linePaints[Math.floor(Math.random() * linePaints.length)], 
        emissive: linePaints[Math.floor(Math.random() * linePaints.length)], 
        emissiveIntensity: 6 
      })
    );
    line.position.set(lineWidth / 2, -index * 0.15, 0);
    return line;
  };

  for (let i = 0; i < 12; i++) {
    const line = createCodeLine(i);
    codeLinesGroup.add(line);
    codeLines.push(line);
  }

  const codeTimer = setInterval(() => {
    const oldLine = codeLines.shift();
    codeLinesGroup.remove(oldLine);
    if (oldLine.geometry) oldLine.geometry.dispose();
    if (oldLine.material) oldLine.material.dispose();
    codeLines.forEach((line, idx) => {
      line.position.y = -idx * 0.15;
    });
    const newLine = createCodeLine(codeLines.length);
    codeLinesGroup.add(newLine);
    codeLines.push(newLine);
  }, 3000);

  // 3. Doll-style Person (Upgraded)
  const personGroup = new THREE.Group();
  personGroup.position.set(0, -0.8, 2.8);
  workspaceGroup.add(personGroup);

  // Body - Hoodie
  const torso = new THREE.Mesh(new THREE.CylinderGeometry(0.6, 0.8, 1.6), clothMat);
  personGroup.add(torso);

  // Hood part
  const hood = new THREE.Mesh(new THREE.SphereGeometry(0.65, 16, 16, 0, Math.PI * 2, 0, Math.PI / 2), clothMat);
  hood.position.y = 0.8;
  personGroup.add(hood);

  // Head - Glossy vinyl look
  headGroup = new THREE.Group();
  headGroup.position.y = 1.35;
  personGroup.add(headGroup);

  const head = new THREE.Mesh(new THREE.SphereGeometry(0.55, 32, 32), skinMat);
  headGroup.add(head);

  // Eyes - Glowing Dots
    // Eyes removed as requested

  // Hair - Stylized capping hair
  const hair = new THREE.Mesh(
    new THREE.SphereGeometry(0.57, 32, 16, 0, Math.PI * 2, 0, Math.PI / 2),
    new THREE.MeshStandardMaterial({ color: 0x050505, roughness: 0.2 })
  );
  hair.rotation.x = -Math.PI * 0.1;
  hair.position.y = 0.05;
  headGroup.add(hair);

  // Arms - Hoodie sleeves with skin hands
  leftArm = new THREE.Group();
  leftArm.position.set(-0.8, 0.5, -0.2);
  personGroup.add(leftArm);
  const leftSleeve = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.2, 1.2), clothMat);
  leftSleeve.rotation.set(Math.PI * 0.35, 0, Math.PI * 0.15);
  leftArm.add(leftSleeve);
  const leftHand = new THREE.Mesh(new THREE.SphereGeometry(0.2, 8, 8), skinMat);
  leftHand.position.set(-0.6, 0, -1.0);
  leftArm.add(leftHand);

  rightArm = new THREE.Group();
  rightArm.position.set(0.8, 0.5, -0.2);
  personGroup.add(rightArm);
  const rightSleeve = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.2, 1.2), clothMat);
  rightSleeve.rotation.set(Math.PI * 0.35, 0, -Math.PI * 0.15);
  rightArm.add(rightSleeve);
  const rightHand = new THREE.Mesh(new THREE.SphereGeometry(0.2, 8, 8), skinMat);
  rightHand.position.set(0.6, 0, -1.0);
  rightArm.add(rightHand);

  // 4. Chair (Fixed/Neon)
  const chairGroup = new THREE.Group();
  chairGroup.position.set(0, -2.1, 2.8);
  workspaceGroup.add(chairGroup);

  const chairSeat = new THREE.Mesh(new THREE.BoxGeometry(1.7, 0.25, 1.7), darkMat);
  chairGroup.add(chairSeat);
  const seatEdges = new THREE.EdgesGeometry(new THREE.BoxGeometry(1.7, 0.25, 1.7));
  const seatLine = new THREE.LineSegments(seatEdges, new THREE.LineBasicMaterial({ color: 0x9d4edd }));
  chairSeat.add(seatLine);

  const chairBack = new THREE.Mesh(new THREE.BoxGeometry(1.7, 2, 0.25), darkMat);
  chairBack.position.set(0, 1.1, 0.85);
  chairGroup.add(chairBack);
  const backEdges = new THREE.EdgesGeometry(new THREE.BoxGeometry(1.7, 2, 0.25));
  const backLine = new THREE.LineSegments(backEdges, new THREE.LineBasicMaterial({ color: 0x9d4edd }));
  chairBack.add(backLine);

  const chairLeg = new THREE.Mesh(new THREE.CylinderGeometry(0.12, 0.12, 1.2), darkMat);
  chairLeg.position.y = -0.6;
  chairGroup.add(chairLeg);
  const legEdges = new THREE.EdgesGeometry(new THREE.CylinderGeometry(0.12, 0.12, 1.2));
  const legLine = new THREE.LineSegments(legEdges, new THREE.LineBasicMaterial({ color: 0x9d4edd }));
  chairLeg.add(legLine);

  // 5. Desk Lamp (Special Glossy Yellow)
  const lampGroup = new THREE.Group();
  lampGroup.position.set(-3.2, -0.85, -1.5);
  workspaceGroup.add(lampGroup);

  const lampBase = new THREE.Mesh(new THREE.CylinderGeometry(0.6, 0.6, 0.1), darkMat);
  lampGroup.add(lampBase);

  const lampArm = new THREE.Mesh(new THREE.CylinderGeometry(0.1, 0.1, 2.6), darkMat);
  lampArm.position.set(0, 1.3, 0);
  lampArm.rotation.z = Math.PI * 0.1;
  lampGroup.add(lampArm);

  const lampHead = new THREE.Mesh(new THREE.CylinderGeometry(0.4, 0.7, 0.9), darkMat);
  lampHead.position.set(0.6, 2.6, 0);
  lampHead.rotation.z = -Math.PI * 0.4;
  lampGroup.add(lampHead);

  const lampBulb = new THREE.Mesh(new THREE.SphereGeometry(0.35, 16, 16), new THREE.MeshStandardMaterial({ color: 0xffd000, emissive: 0xffd000, emissiveIntensity: 20 }));
  lampBulb.position.set(0.7, 2.6, 0);
  lampGroup.add(lampBulb);

  const lampLight = new THREE.PointLight(0xffd000, 50, 15);
  lampLight.position.set(1.5, 2.6, 1);
  lampGroup.add(lampLight);

  // 6. Coffee Mug (Yellow Radiant)
  const mugGroup = new THREE.Group();
  mugGroup.position.set(2.8, -0.7, 0.8);
  workspaceGroup.add(mugGroup);
  const mug = new THREE.Mesh(new THREE.CylinderGeometry(0.28, 0.28, 0.6), neonYellowMat);
  mugGroup.add(mug);
  const mugHandle = new THREE.Mesh(new THREE.TorusGeometry(0.18, 0.06, 8, 16), neonYellowMat);
  mugHandle.position.x = 0.25;
  mugGroup.add(mugHandle);

  // 7. Notebook
  const notebook = new THREE.Mesh(new THREE.BoxGeometry(1, 0.1, 1.2), new THREE.MeshStandardMaterial({ color: 0xffffff, roughness: 0.3 }));
  notebook.position.set(-1.8, -0.84, 0.8);
  notebook.rotation.y = -Math.PI * 0.1;
  workspaceGroup.add(notebook);
  const notebookCover = new THREE.Mesh(new THREE.BoxGeometry(1.02, 0.06, 1.22), darkMat);
  notebookCover.position.y = -0.04;
  notebook.add(notebookCover);

  // --- Interaction & Theme ---
  const mouse = { x: 0, y: 0 };
  const targetRotation = { x: 0, y: 0 };

  const handleMouseMove = (event) => {
    mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
    mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;
  };
  window.addEventListener('mousemove', handleMouseMove);

  const updateLampForTheme = (theme) => {
    const isDarkTheme = theme === 'dark';
    if (lampLight) lampLight.intensity = isDarkTheme ? 50 : 2;
    if (lampBulb && lampBulb.material) {
      lampBulb.material.emissiveIntensity = isDarkTheme ? 20 : 0.5;
    }
  };

  const observer = new MutationObserver((mutations) => {
    mutations.forEach((mutation) => {
      if (mutation.attributeName === 'data-theme') {
        updateLampForTheme(document.documentElement.getAttribute('data-theme'));
      }
    });
  });
  observer.observe(document.documentElement, { attributes: true });
  updateLampForTheme(document.documentElement.getAttribute('data-theme') || 'dark');

  const animate = (time) => {
    animationFrame = requestAnimationFrame(animate);

    targetRotation.x += (mouse.y * 0.12 - targetRotation.x) * 0.05;
    targetRotation.y += (mouse.x * 0.12 - targetRotation.y) * 0.05;

    workspaceGroup.rotation.x = targetRotation.x + 0.15;
    workspaceGroup.rotation.y = targetRotation.y + 0.15;

    // Movement for person
    const t = time * 0.005;
    headGroup.position.y = 1.35 + Math.sin(t) * 0.02;
    leftArm.rotation.x = Math.sin(t * 1.6) * 0.08;
    rightArm.rotation.x = Math.cos(t * 1.6) * 0.08;

    renderer.render(scene, camera);
  };
  animate();

  const handleResize = () => {
    if (!container.value) return;
    camera.aspect = container.value.clientWidth / container.value.clientHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(container.value.clientWidth, container.value.clientHeight);
  };
  window.addEventListener('resize', handleResize);

  onUnmounted(() => {
    clearInterval(codeTimer);
    observer.disconnect();
    cancelAnimationFrame(animationFrame);
    window.removeEventListener('mousemove', handleMouseMove);
    window.removeEventListener('resize', handleResize);
    renderer.dispose();
  });
};

onMounted(init);
</script>

<template>
  <div ref="container" class="radium-canvas-container"></div>
</template>

<style scoped>
.radium-canvas-container {
  width: 100%;
  height: 550px;
}

@media (max-width: 768px) {
  .radium-canvas-container {
    height: 500px;
  }
}
</style>
