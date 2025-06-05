<script setup>
import CssArt from './pages/CssArt.vue';
import RealisticArt from './pages/RealisticArt.vue';
import FamousArt from './pages/FamousArt.vue';
import RembrandtArt from './pages/RembrandtArt.vue';
import ModernArt from './pages/ModernArt.vue';
import ColorPalette from './pages/ColorPalette.vue';
import ContrastChecker from './pages/ContrastChecker.vue';
import FontExplorer from './pages/FontExplorer.vue';
import TypographyPairing from './pages/TypographyPairing.vue';
import DesignSystemGenerator from './pages/DesignSystemGenerator.vue';
import { ref } from 'vue';

const currentPage = ref('abstract');

function switchPage(page) {
  currentPage.value = page;
}
</script>

<template>
  <div class="app-container">
    <header>
      <h1>Artsy</h1>
      <nav>
        <button 
          :class="{ active: currentPage === 'abstract' }" 
          @click="switchPage('abstract')">Abstract Art</button>
        <button 
          :class="{ active: currentPage === 'realistic' }" 
          @click="switchPage('realistic')">Realistic Art</button>
        <button 
          :class="{ active: currentPage === 'famous' }" 
          @click="switchPage('famous')">Famous Paintings</button>
        <button 
          :class="{ active: currentPage === 'rembrandt' }" 
          @click="switchPage('rembrandt')">The Night Watch</button>
        <button 
          :class="{ active: currentPage === 'modern' }" 
          @click="switchPage('modern')">Neo-Mondrian</button>
        <button 
          :class="{ active: currentPage === 'palette' }" 
          @click="switchPage('palette')">Color Palette</button>
        <button 
          :class="{ active: currentPage === 'contrast' }" 
          @click="switchPage('contrast')">Contrast Checker</button>
        <button 
          :class="{ active: currentPage === 'fonts' }" 
          @click="switchPage('fonts')">Font Explorer</button>
        <button 
          :class="{ active: currentPage === 'typography' }" 
          @click="switchPage('typography')">Typography Pairing</button>
        <button 
          :class="{ active: currentPage === 'design-system' }" 
          @click="switchPage('design-system')">Design System</button>
      </nav>
    </header>
    <main>
      <CssArt v-if="currentPage === 'abstract'" />
      <RealisticArt v-if="currentPage === 'realistic'" />
      <FamousArt v-if="currentPage === 'famous'" />
      <RembrandtArt v-if="currentPage === 'rembrandt'" />
      <ModernArt v-if="currentPage === 'modern'" />
      <ColorPalette v-if="currentPage === 'palette'" />
      <ContrastChecker v-if="currentPage === 'contrast'" />
      <FontExplorer v-if="currentPage === 'fonts'" />
      <TypographyPairing v-if="currentPage === 'typography'" />
      <DesignSystemGenerator v-if="currentPage === 'design-system'" />
    </main>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background-color: #f9f9f9;
  color: #333;
}

.app-container {
  min-height: 100vh;
}

header {
  background-color: #333;
  color: white;
  padding: 1rem;
  text-align: center;
}

nav {
  margin-top: 1rem;
}

button {
  background-color: #555;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  margin: 0 0.5rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #777;
}

button.active {
  background-color: #e91e63;
}

main {
  padding: 1rem;
}
</style>
