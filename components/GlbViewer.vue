<script setup lang="ts">
import { OrbitControls, GLTFModel } from '@tresjs/cientos'
import { TresCanvas } from '@tresjs/core'
</script>

<template>
  <TresCanvas alpha clear-color="transparent" window-size style="position: absolute; top: 0; left: 0; right: 0; bottom: 0;"> <!-- Adjusted canvas properties -->
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




  