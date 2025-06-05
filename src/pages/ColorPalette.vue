<template>
  <div class="color-palette-container">
    <h1>Color Palette Generator</h1>
    <p class="instructions">Press the spacebar to generate a new color palette</p>
    
    <!-- Main palette display -->
    <div class="palette-display" tabindex="0" @keydown="handleKeydown" ref="paletteRef">
      <div 
        v-for="(color, index) in colors" 
        :key="index" 
        class="color-column"
        :class="{ 'showing-shades': showShades[index] }"
        :style="{ backgroundColor: showShades[index] ? 'transparent' : color }"
        @click="toggleShades(index)"
      >
        <!-- Show color info when not showing shades -->
        <div v-if="!showShades[index]" class="color-info">
          <span class="color-hex">{{ color }}</span>
          <button class="copy-btn" @click.stop="copyToClipboard(color)">Copy</button>
        </div>
        
        <!-- Shade pills if shades are toggled for this column -->
        <div v-if="showShades[index]" class="shades-container">
          <div class="shades-header">
            <span>Shades of {{ color }}</span>
            <button class="close-shades-btn" @click.stop="toggleShades(index)">×</button>
          </div>
          <div 
            v-for="(shade, shadeIndex) in generateShadesForColor(color)" 
            :key="shadeIndex" 
            class="shade-pill"
            :style="{ backgroundColor: shade }"
            @click.stop="copyToClipboard(shade)"
          >
            <span class="shade-label">{{ shade }}</span>
          </div>
        </div>
      </div>
    </div>
    
    <div class="palette-controls">
      <button @click="generatePalette" class="generate-btn">Generate New Palette</button>
      <div class="palette-options">
        <label>
          <input type="radio" v-model="paletteType" value="random" @change="generatePalette"> 
          Random
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="analogous" @change="generatePalette"> 
          Analogous
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="monochromatic" @change="generatePalette"> 
          Monochromatic
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="complementary" @change="generatePalette"> 
          Complementary
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="triadic" @change="generatePalette"> 
          Triadic
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="tetradic" @change="generatePalette"> 
          Tetradic
        </label>
        <label>
          <input type="radio" v-model="paletteType" value="splitComplementary" @change="generatePalette"> 
          Split-Complementary
        </label>
      </div>
      <div class="columns-control">
        <label>Columns: 
          <select v-model="numColumns" @change="generatePalette">
            <option>3</option>
            <option>4</option>
            <option>5</option>
            <option>6</option>
          </select>
        </label>
      </div>
      <div class="tip-container">
        <p class="tip">Pro Tip: Click on any color to see 10 shades of that color</p>
      </div>
    </div>
    
    <div class="saved-palettes">
      <h2>Saved Palettes</h2>
      <div class="save-current">
        <button @click="savePalette" class="save-btn">Save Current Palette</button>
      </div>
      <div v-if="savedPalettes.length === 0" class="no-saved">No saved palettes yet</div>
      <div v-else class="palette-grid">
        <div 
          v-for="(palette, pIndex) in savedPalettes" 
          :key="pIndex"
          class="saved-palette"
        >
          <div class="saved-colors">
            <div 
              v-for="(color, cIndex) in palette" 
              :key="cIndex"
              class="saved-color"
              :style="{ backgroundColor: color }"
            ></div>
          </div>
          <div class="saved-actions">
            <button @click="loadPalette(palette)">Load</button>
            <button @click="removePalette(pIndex)">Remove</button>
          </div>
        </div>
      </div>
    </div>
    
    <div class="toast" :class="{ 'show-toast': showToast }">
      Copied to clipboard!
    </div>
  </div>
</template>

<script>
export default {
  name: 'ColorPalette',
  data() {
    return {
      colors: [],
      savedPalettes: [],
      paletteType: 'random',
      numColumns: 5,
      showToast: false,
      showShades: {} // Tracks which columns are showing shades
    }
  },
  mounted() {
    this.generatePalette();
    this.$refs.paletteRef.focus();
    
    // Load saved palettes from localStorage if available
    const savedPalettes = localStorage.getItem('savedPalettes');
    if (savedPalettes) {
      this.savedPalettes = JSON.parse(savedPalettes);
    }
  },
  methods: {
    handleKeydown(event) {
      if (event.code === 'Space') {
        event.preventDefault();
        this.generatePalette();
      }
    },
    generatePalette() {
      this.colors = [];
      this.showShades = {}; // Reset shades display when generating new palette
      
      switch(this.paletteType) {
        case 'random':
          this.generateRandomPalette();
          break;
        case 'analogous':
          this.generateAnalogousPalette();
          break;
        case 'monochromatic':
          this.generateMonochromaticPalette();
          break;
        case 'complementary':
          this.generateComplementaryPalette();
          break;
        case 'triadic':
          this.generateTriadicPalette();
          break;
        case 'tetradic':
          this.generateTetradicPalette();
          break;
        case 'splitComplementary':
          this.generateSplitComplementaryPalette();
          break;
        default:
          this.generateRandomPalette();
      }
    },
    generateRandomPalette() {
      for (let i = 0; i < this.numColumns; i++) {
        const color = this.getRandomHexColor();
        this.colors.push(color);
      }
    },
    generateAnalogousPalette() {
      // Generate analogous colors based on a random hue
      const baseHue = Math.floor(Math.random() * 360);
      const saturation = 70 + Math.floor(Math.random() * 30);
      const lightness = 50 + Math.floor(Math.random() * 20);
      
      for (let i = 0; i < this.numColumns; i++) {
        // Distribute hues evenly around the base hue
        const hueOffset = (i - Math.floor(this.numColumns / 2)) * (30 / this.numColumns);
        let hue = (baseHue + hueOffset) % 360;
        if (hue < 0) hue += 360;
        
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    generateMonochromaticPalette() {
      // Generate monochromatic colors based on a random hue
      const hue = Math.floor(Math.random() * 360);
      const saturation = 70 + Math.floor(Math.random() * 30);
      
      for (let i = 0; i < this.numColumns; i++) {
        // Distribute lightness evenly
        const lightness = 20 + (i * (60 / this.numColumns));
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    generateComplementaryPalette() {
      // Generate complementary colors
      const baseHue = Math.floor(Math.random() * 360);
      const complementaryHue = (baseHue + 180) % 360;
      
      // Generate colors around both hues
      for (let i = 0; i < this.numColumns; i++) {
        let hue, saturation, lightness;
        
        if (i < this.numColumns / 2) {
          // Colors around the base hue
          hue = (baseHue + (i * 15) - 15) % 360;
          saturation = 70 + Math.floor(Math.random() * 30);
          lightness = 40 + (i * 10);
        } else {
          // Colors around the complementary hue
          hue = (complementaryHue + ((i - Math.floor(this.numColumns / 2)) * 15) - 15) % 360;
          saturation = 70 + Math.floor(Math.random() * 30);
          lightness = 40 + ((i - Math.floor(this.numColumns / 2)) * 10);
        }
        
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    generateTriadicPalette() {
      // Generate triadic colors (three colors equally spaced around the color wheel)
      const baseHue = Math.floor(Math.random() * 360);
      const triad2 = (baseHue + 120) % 360;
      const triad3 = (baseHue + 240) % 360;
      
      const baseSaturation = 70 + Math.floor(Math.random() * 30);
      const baseLightness = 50 + Math.floor(Math.random() * 20);
      
      // Create variations around each of the three main colors
      for (let i = 0; i < this.numColumns; i++) {
        let hue, saturation, lightness;
        
        // Determine which triad group this color belongs to
        const triadGroup = Math.floor(i * 3 / this.numColumns);
        const positionInGroup = i - (triadGroup * Math.ceil(this.numColumns / 3));
        
        switch(triadGroup) {
          case 0:
            hue = (baseHue + positionInGroup * 10) % 360;
            break;
          case 1:
            hue = (triad2 + positionInGroup * 10) % 360;
            break;
          case 2:
            hue = (triad3 + positionInGroup * 10) % 360;
            break;
        }
        
        saturation = baseSaturation - (positionInGroup * 5);
        lightness = baseLightness - (positionInGroup * 5);
        
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    generateTetradicPalette() {
      // Generate tetradic colors (four colors forming a rectangle on the color wheel)
      const baseHue = Math.floor(Math.random() * 360);
      const tetrad2 = (baseHue + 90) % 360;
      const tetrad3 = (baseHue + 180) % 360;
      const tetrad4 = (baseHue + 270) % 360;
      
      const baseSaturation = 70 + Math.floor(Math.random() * 30);
      const baseLightness = 50 + Math.floor(Math.random() * 20);
      
      // Create variations around each of the four main colors
      for (let i = 0; i < this.numColumns; i++) {
        let hue;
        
        // Determine which tetrad group this color belongs to
        const tetradGroup = Math.floor(i * 4 / this.numColumns);
        const variationFactor = (i % Math.ceil(this.numColumns / 4)) * 5;
        
        switch(tetradGroup) {
          case 0:
            hue = (baseHue + variationFactor) % 360;
            break;
          case 1:
            hue = (tetrad2 + variationFactor) % 360;
            break;
          case 2:
            hue = (tetrad3 + variationFactor) % 360;
            break;
          case 3:
            hue = (tetrad4 + variationFactor) % 360;
            break;
        }
        
        const saturation = baseSaturation - variationFactor;
        const lightness = baseLightness;
        
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    generateSplitComplementaryPalette() {
      // Generate split-complementary colors (a base color and two colors adjacent to its complement)
      const baseHue = Math.floor(Math.random() * 360);
      const complementaryHue = (baseHue + 180) % 360;
      const splitComp1 = (complementaryHue - 30) % 360;
      const splitComp2 = (complementaryHue + 30) % 360;
      
      const baseSaturation = 70 + Math.floor(Math.random() * 30);
      const baseLightness = 50 + Math.floor(Math.random() * 20);
      
      // Create variations around each of the three main colors
      for (let i = 0; i < this.numColumns; i++) {
        let hue, saturation, lightness;
        
        // Determine which group this color belongs to
        const group = Math.floor(i * 3 / this.numColumns);
        const variationFactor = (i % Math.ceil(this.numColumns / 3)) * 8;
        
        switch(group) {
          case 0:
            hue = (baseHue + variationFactor) % 360;
            saturation = baseSaturation;
            lightness = baseLightness;
            break;
          case 1:
            hue = (splitComp1 + variationFactor) % 360;
            saturation = baseSaturation - 5;
            lightness = baseLightness - 5;
            break;
          case 2:
            hue = (splitComp2 + variationFactor) % 360;
            saturation = baseSaturation - 10;
            lightness = baseLightness - 10;
            break;
        }
        
        const color = this.hslToHex(hue, saturation, lightness);
        this.colors.push(color);
      }
    },
    toggleShades(columnIndex) {
      // Toggle shades for the clicked column
      this.showShades = {
        ...this.showShades,
        [columnIndex]: !this.showShades[columnIndex]
      };
    },
    generateShadesForColor(hexColor) {
      // Convert hex to HSL
      const r = parseInt(hexColor.slice(1, 3), 16) / 255;
      const g = parseInt(hexColor.slice(3, 5), 16) / 255;
      const b = parseInt(hexColor.slice(5, 7), 16) / 255;
      
      const max = Math.max(r, g, b);
      const min = Math.min(r, g, b);
      let h, s, l = (max + min) / 2;
      
      if (max === min) {
        h = s = 0; // achromatic
      } else {
        const d = max - min;
        s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
        
        switch (max) {
          case r: h = (g - b) / d + (g < b ? 6 : 0); break;
          case g: h = (b - r) / d + 2; break;
          case b: h = (r - g) / d + 4; break;
        }
        
        h /= 6;
      }
      
      h = Math.round(h * 360);
      s = Math.round(s * 100);
      l = Math.round(l * 100);
      
      // Generate 10 shades
      const shades = [];
      for (let i = 0; i < 10; i++) {
        // Vary lightness from 5% to 95%
        const newLightness = 5 + (i * 10);
        shades.push(this.hslToHex(h, s, newLightness));
      }
      
      return shades;
    },
    getRandomHexColor() {
      return '#' + Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0');
    },
    copyToClipboard(color) {
      navigator.clipboard.writeText(color).then(() => {
        this.showToast = true;
        setTimeout(() => {
          this.showToast = false;
        }, 2000);
      });
    },
    savePalette() {
      this.savedPalettes.push([...this.colors]);
      localStorage.setItem('savedPalettes', JSON.stringify(this.savedPalettes));
    },
    loadPalette(palette) {
      this.colors = [...palette];
    },
    removePalette(index) {
      this.savedPalettes.splice(index, 1);
      localStorage.setItem('savedPalettes', JSON.stringify(this.savedPalettes));
    },
    hslToHex(h, s, l) {
      l /= 100;
      const a = s * Math.min(l, 1 - l) / 100;
      const f = n => {
        const k = (n + h / 30) % 12;
        const color = l - a * Math.max(Math.min(k - 3, 9 - k, 1), -1);
        return Math.round(255 * color).toString(16).padStart(2, '0');
      };
      return `#${f(0)}${f(8)}${f(4)}`;
    }
  }
}
</script>

<style scoped>
.color-palette-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

h1, h2 {
  text-align: center;
  color: #333;
}

.instructions {
  text-align: center;
  color: #666;
  margin-bottom: 30px;
}

.palette-display {
  display: flex;
  height: 300px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
  outline: none;
}

.color-column {
  flex: 1;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  position: relative;
  transition: all 0.3s ease;
  cursor: pointer;
}

.color-column:not(.showing-shades):hover {
  transform: translateY(-10px);
}

.color-info {
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 15px;
  margin-bottom: 20px;
  border-radius: 4px;
  text-align: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
}

.color-column:hover .color-info {
  opacity: 1;
}

/* Shades styling */
.showing-shades {
  z-index: 5;
}

.shades-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  background: white;
  padding: 5px;
  position: relative;
  overflow-y: auto;
}

.shades-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px;
  background-color: #f5f5f5;
  border-bottom: 1px solid #ddd;
  position: sticky;
  top: 0;
  z-index: 2;
}

.close-shades-btn {
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  color: #666;
}

.close-shades-btn:hover {
  color: #333;
}

.shade-pill {
  flex: 1;
  margin: 2px 0;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  position: relative;
  transition: transform 0.2s;
  border-radius: 4px;
}

.shade-pill:hover {
  transform: translateX(5px);
}

.shade-label {
  color: white;
  font-size: 11px;
  font-family: monospace;
  text-shadow: 0 0 2px rgba(0, 0, 0, 0.8);
  opacity: 0;
  transition: opacity 0.2s;
}

.shade-pill:hover .shade-label {
  opacity: 1;
}

.tip-container {
  margin-top: 15px;
}

.tip {
  font-style: italic;
  color: #666;
  font-size: 14px;
}

.save-current {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.save-btn {
  background-color: #2196f3;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.save-btn:hover {
  background-color: #0d8bf2;
}

.palette-controls {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 30px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.generate-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin-bottom: 15px;
}

.generate-btn:hover {
  background-color: #45a049;
}

.palette-options {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 12px;
  margin-bottom: 15px;
  max-width: 100%;
}

.palette-options label {
  display: flex;
  align-items: center;
  background-color: white;
  padding: 6px 12px;
  border-radius: 20px;
  border: 1px solid #ddd;
  cursor: pointer;
  transition: all 0.2s ease;
}

.palette-options label:hover {
  border-color: #2196f3;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.palette-options input[type="radio"] {
  margin-right: 5px;
}

.columns-control {
  margin-bottom: 15px;
}

.columns-control select {
  margin-left: 5px;
  padding: 5px;
  border-radius: 4px;
  border: 1px solid #ddd;
}

.saved-palettes {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 30px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.saved-palettes h2 {
  margin-top: 0;
  margin-bottom: 20px;
}

.no-saved {
  text-align: center;
  color: #666;
  font-style: italic;
  padding: 20px;
}

.palette-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 15px;
  margin-top: 15px;
}

.saved-palette {
  background-color: white;
  border-radius: 6px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.saved-palette:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.saved-colors {
  display: flex;
  height: 80px;
}

.saved-color {
  flex: 1;
}

.saved-actions {
  display: flex;
  padding: 10px;
  justify-content: space-between;
  background-color: #f9f9f9;
}

.saved-actions button {
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.saved-actions button:first-child {
  background-color: #2196f3;
  color: white;
}

.saved-actions button:last-child {
  background-color: #f44336;
  color: white;
}

.toast {
  position: fixed;
  bottom: -50px;
  left: 50%;
  transform: translateX(-50%);
  background-color: #333;
  color: white;
  padding: 12px 24px;
  border-radius: 4px;
  transition: bottom 0.3s;
  z-index: 1000;
}

.show-toast {
  bottom: 20px;
}

/* Add responsive styling for mobile */
@media (max-width: 768px) {
  .palette-options {
    gap: 8px;
  }
  
  .palette-options label {
    padding: 4px 8px;
    font-size: 14px;
  }
  
  .palette-grid {
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  }
}
</style>