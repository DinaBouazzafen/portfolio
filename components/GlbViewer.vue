<script setup lang="ts">
import { OrbitControls, GLTFModel } from '@tresjs/cientos'
import { TresCanvas } from '@tresjs/core'
</script>

<template>
  <TresCanvas alpha clear-color="transparent" window-size :styles="{ pointerEvents: 'auto' }">
        <OrbitControls />
    <TresPerspectiveCamera :position="[0, 0, 5]" />

    <!-- Your 3D Model -->
    <Suspense>
      <GLTFModel 
        path="/img/me.glb" 
        :position="[0, -1, 0]"
      />
    </Suspense>

    <!-- Lights to illuminate the model -->
    <TresAmbientLight :intensity="2" />
    <TresDirectionalLight :position="[0, -1, 0]" :intensity="2" />
  </TresCanvas>
</template>






  