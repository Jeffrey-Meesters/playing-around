<template>
  <div class="contrast-checker-container">
    <h1>Contrast Checker</h1>
    <p class="instructions">Check if your color combinations meet accessibility standards</p>
    
    <div class="checker-grid">
      <!-- Color inputs section -->
      <div class="color-inputs">
        <div class="color-input-group">
          <h3>Foreground Color</h3>
          <div class="input-row">
            <input 
              type="color" 
              v-model="foregroundColor" 
              class="color-picker"
            />
            <input 
              type="text" 
              v-model="foregroundColor" 
              class="color-text-input"
              @input="validateHexInput('foregroundColor')"
            />
          </div>
          <div class="color-format-toggles">
            <button @click="switchToFormat('foreground', 'hex')" :class="{ active: foregroundFormat === 'hex' }">HEX</button>
            <button @click="switchToFormat('foreground', 'rgb')" :class="{ active: foregroundFormat === 'rgb' }">RGB</button>
            <button @click="switchToFormat('foreground', 'hsl')" :class="{ active: foregroundFormat === 'hsl' }">HSL</button>
          </div>
          <div v-if="foregroundFormat === 'rgb'" class="slider-controls">
            <label>
              R: {{ foregroundRGB.r }}
              <input type="range" v-model.number="foregroundRGB.r" min="0" max="255" @input="updateFromRGB('foreground')">
            </label>
            <label>
              G: {{ foregroundRGB.g }}
              <input type="range" v-model.number="foregroundRGB.g" min="0" max="255" @input="updateFromRGB('foreground')">
            </label>
            <label>
              B: {{ foregroundRGB.b }}
              <input type="range" v-model.number="foregroundRGB.b" min="0" max="255" @input="updateFromRGB('foreground')">
            </label>
          </div>
          <div v-if="foregroundFormat === 'hsl'" class="slider-controls">
            <label>
              H: {{ foregroundHSL.h }}°
              <input type="range" v-model.number="foregroundHSL.h" min="0" max="360" @input="updateFromHSL('foreground')">
            </label>
            <label>
              S: {{ foregroundHSL.s }}%
              <input type="range" v-model.number="foregroundHSL.s" min="0" max="100" @input="updateFromHSL('foreground')">
            </label>
            <label>
              L: {{ foregroundHSL.l }}%
              <input type="range" v-model.number="foregroundHSL.l" min="0" max="100" @input="updateFromHSL('foreground')">
            </label>
          </div>
        </div>

        <div class="color-input-group">
          <h3>Background Color</h3>
          <div class="input-row">
            <input 
              type="color" 
              v-model="backgroundColor" 
              class="color-picker"
            />
            <input 
              type="text" 
              v-model="backgroundColor" 
              class="color-text-input"
              @input="validateHexInput('backgroundColor')"
            />
          </div>
          <div class="color-format-toggles">
            <button @click="switchToFormat('background', 'hex')" :class="{ active: backgroundFormat === 'hex' }">HEX</button>
            <button @click="switchToFormat('background', 'rgb')" :class="{ active: backgroundFormat === 'rgb' }">RGB</button>
            <button @click="switchToFormat('background', 'hsl')" :class="{ active: backgroundFormat === 'hsl' }">HSL</button>
          </div>
          <div v-if="backgroundFormat === 'rgb'" class="slider-controls">
            <label>
              R: {{ backgroundRGB.r }}
              <input type="range" v-model.number="backgroundRGB.r" min="0" max="255" @input="updateFromRGB('background')">
            </label>
            <label>
              G: {{ backgroundRGB.g }}
              <input type="range" v-model.number="backgroundRGB.g" min="0" max="255" @input="updateFromRGB('background')">
            </label>
            <label>
              B: {{ backgroundRGB.b }}
              <input type="range" v-model.number="backgroundRGB.b" min="0" max="255" @input="updateFromRGB('background')">
            </label>
          </div>
          <div v-if="backgroundFormat === 'hsl'" class="slider-controls">
            <label>
              H: {{ backgroundHSL.h }}°
              <input type="range" v-model.number="backgroundHSL.h" min="0" max="360" @input="updateFromHSL('background')">
            </label>
            <label>
              S: {{ backgroundHSL.s }}%
              <input type="range" v-model.number="backgroundHSL.s" min="0" max="100" @input="updateFromHSL('background')">
            </label>
            <label>
              L: {{ backgroundHSL.l }}%
              <input type="range" v-model.number="backgroundHSL.l" min="0" max="100" @input="updateFromHSL('background')">
            </label>
          </div>
        </div>

        <div class="swap-colors">
          <button @click="swapColors" class="swap-btn">Swap Colors</button>
        </div>
      </div>
      
      <!-- Preview and contrast ratio section -->
      <div class="preview-section">
        <div class="preview-box" :style="{ backgroundColor: backgroundColor, color: foregroundColor }">
          <div class="preview-text">
            <h2>Preview Text</h2>
            <p class="large-text">Large Text (18pt bold or 24pt normal)</p>
            <p class="normal-text">Normal text (under 18pt)</p>
          </div>
        </div>
        
        <div class="contrast-results">
          <div class="contrast-ratio">
            <h3>Contrast Ratio</h3>
            <div class="ratio-display">{{ contrastRatio }}:1</div>
          </div>
          
          <div class="wcag-results">
            <h3>WCAG 2.1 Compliance</h3>
            <div class="compliance-item">
              <div class="level">AA</div>
              <div class="compliance-details">
                <div :class="{ pass: isAALargeText, fail: !isAALargeText }">
                  <span class="status-icon">{{ isAALargeText ? '✓' : '✗' }}</span> Large Text
                </div>
                <div :class="{ pass: isAANormalText, fail: !isAANormalText }">
                  <span class="status-icon">{{ isAANormalText ? '✓' : '✗' }}</span> Normal Text
                </div>
                <div :class="{ pass: isAAUI, fail: !isAAUI }">
                  <span class="status-icon">{{ isAAUI ? '✓' : '✗' }}</span> UI Components
                </div>
              </div>
            </div>
            
            <div class="compliance-item">
              <div class="level">AAA</div>
              <div class="compliance-details">
                <div :class="{ pass: isAAALargeText, fail: !isAAALargeText }">
                  <span class="status-icon">{{ isAAALargeText ? '✓' : '✗' }}</span> Large Text
                </div>
                <div :class="{ pass: isAAANormalText, fail: !isAAANormalText }">
                  <span class="status-icon">{{ isAAANormalText ? '✓' : '✗' }}</span> Normal Text
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <div class="saved-combos">
      <h2>Saved Color Combinations</h2>
      <div class="save-current">
        <button @click="saveCombo" class="save-btn">Save Current Combination</button>
      </div>
      <div v-if="savedCombos.length === 0" class="no-saved">No saved combinations yet</div>
      <div v-else class="combos-grid">
        <div 
          v-for="(combo, index) in savedCombos" 
          :key="index"
          class="saved-combo"
        >
          <div 
            class="combo-preview" 
            :style="{ backgroundColor: combo.background, color: combo.foreground }"
          >
            <span class="combo-text">Aa</span>
          </div>
          <div class="combo-details">
            <div class="combo-colors">
              <div class="combo-color">
                <span class="color-label">Foreground:</span> 
                <span class="color-value">{{ combo.foreground }}</span>
              </div>
              <div class="combo-color">
                <span class="color-label">Background:</span> 
                <span class="color-value">{{ combo.background }}</span>
              </div>
              <div class="combo-ratio">
                <span class="ratio-value">{{ combo.ratio }}:1</span>
                <span class="combo-compliance" :class="{ 'pass': combo.passesAA }">
                  {{ combo.passesAA ? 'AA Pass' : 'AA Fail' }}
                </span>
              </div>
            </div>
            <div class="combo-actions">
              <button @click="loadCombo(combo)">Load</button>
              <button @click="removeCombo(index)" class="remove-btn">Remove</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContrastChecker',
  data() {
    return {
      foregroundColor: '#FFFFFF',
      backgroundColor: '#121212',
      foregroundFormat: 'hex',
      backgroundFormat: 'hex',
      foregroundRGB: { r: 255, g: 255, b: 255 },
      backgroundRGB: { r: 18, g: 18, b: 18 },
      foregroundHSL: { h: 0, s: 0, l: 100 },
      backgroundHSL: { h: 0, s: 0, l: 7 },
      savedCombos: []
    }
  },
  computed: {
    contrastRatio() {
      const luminance1 = this.calculateLuminance(this.foregroundColor);
      const luminance2 = this.calculateLuminance(this.backgroundColor);
      
      const brightest = Math.max(luminance1, luminance2);
      const darkest = Math.min(luminance1, luminance2);
      
      return ((brightest + 0.05) / (darkest + 0.05)).toFixed(2);
    },
    isAALargeText() {
      return parseFloat(this.contrastRatio) >= 3;
    },
    isAANormalText() {
      return parseFloat(this.contrastRatio) >= 4.5;
    },
    isAAUI() {
      return parseFloat(this.contrastRatio) >= 3;
    },
    isAAALargeText() {
      return parseFloat(this.contrastRatio) >= 4.5;
    },
    isAAANormalText() {
      return parseFloat(this.contrastRatio) >= 7;
    }
  },
  mounted() {
    // Initialize RGB and HSL values
    this.updateColorFormats('foreground');
    this.updateColorFormats('background');
    
    // Load saved combinations from localStorage if available
    const savedCombos = localStorage.getItem('savedContrastCombos');
    if (savedCombos) {
      this.savedCombos = JSON.parse(savedCombos);
    }
  },
  methods: {
    calculateLuminance(hexColor) {
      // Convert hex to RGB
      const r = parseInt(hexColor.slice(1, 3), 16) / 255;
      const g = parseInt(hexColor.slice(3, 5), 16) / 255;
      const b = parseInt(hexColor.slice(5, 7), 16) / 255;
      
      // Calculate luminance
      const rgb = [r, g, b].map(c => {
        if (c <= 0.03928) {
          return c / 12.92;
        }
        return Math.pow((c + 0.055) / 1.055, 2.4);
      });
      
      return 0.2126 * rgb[0] + 0.7152 * rgb[1] + 0.0722 * rgb[2];
    },
    validateHexInput(colorProp) {
      // Ensure the hex input is valid
      let color = this[colorProp];
      
      // Add # if missing
      if (color.charAt(0) !== '#') {
        color = '#' + color;
      }
      
      // Validate hex format
      const hexRegex = /^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/;
      if (!hexRegex.test(color)) {
        // Revert to previous valid color if invalid
        if (colorProp === 'foregroundColor') {
          color = '#FFFFFF';
        } else {
          color = '#121212';
        }
      }
      
      // Update the color
      this[colorProp] = color;
      
      // Update RGB and HSL values
      this.updateColorFormats(colorProp === 'foregroundColor' ? 'foreground' : 'background');
    },
    hexToRgb(hex) {
      // Remove # if present
      hex = hex.replace('#', '');
      
      // Convert short hex to full format
      if (hex.length === 3) {
        hex = hex.split('').map(c => c + c).join('');
      }
      
      const r = parseInt(hex.substring(0, 2), 16);
      const g = parseInt(hex.substring(2, 4), 16);
      const b = parseInt(hex.substring(4, 6), 16);
      
      return { r, g, b };
    },
    rgbToHex(r, g, b) {
      return '#' + [r, g, b]
        .map(x => {
          const hex = Math.round(x).toString(16);
          return hex.length === 1 ? '0' + hex : hex;
        })
        .join('');
    },
    rgbToHsl(r, g, b) {
      r /= 255;
      g /= 255;
      b /= 255;
      
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
      
      return {
        h: Math.round(h * 360),
        s: Math.round(s * 100),
        l: Math.round(l * 100)
      };
    },
    hslToRgb(h, s, l) {
      h /= 360;
      s /= 100;
      l /= 100;
      
      let r, g, b;
      
      if (s === 0) {
        r = g = b = l; // achromatic
      } else {
        const hue2rgb = (p, q, t) => {
          if (t < 0) t += 1;
          if (t > 1) t -= 1;
          if (t < 1/6) return p + (q - p) * 6 * t;
          if (t < 1/2) return q;
          if (t < 2/3) return p + (q - p) * (2/3 - t) * 6;
          return p;
        };
        
        const q = l < 0.5 ? l * (1 + s) : l + s - l * s;
        const p = 2 * l - q;
        
        r = hue2rgb(p, q, h + 1/3);
        g = hue2rgb(p, q, h);
        b = hue2rgb(p, q, h - 1/3);
      }
      
      return {
        r: Math.round(r * 255),
        g: Math.round(g * 255),
        b: Math.round(b * 255)
      };
    },
    updateColorFormats(type) {
      const colorValue = type === 'foreground' ? this.foregroundColor : this.backgroundColor;
      const rgb = this.hexToRgb(colorValue);
      
      if (type === 'foreground') {
        this.foregroundRGB = rgb;
        this.foregroundHSL = this.rgbToHsl(rgb.r, rgb.g, rgb.b);
      } else {
        this.backgroundRGB = rgb;
        this.backgroundHSL = this.rgbToHsl(rgb.r, rgb.g, rgb.b);
      }
    },
    switchToFormat(type, format) {
      if (type === 'foreground') {
        this.foregroundFormat = format;
      } else {
        this.backgroundFormat = format;
      }
    },
    updateFromRGB(type) {
      const rgb = type === 'foreground' ? this.foregroundRGB : this.backgroundRGB;
      const hexColor = this.rgbToHex(rgb.r, rgb.g, rgb.b);
      
      if (type === 'foreground') {
        this.foregroundColor = hexColor;
        this.foregroundHSL = this.rgbToHsl(rgb.r, rgb.g, rgb.b);
      } else {
        this.backgroundColor = hexColor;
        this.backgroundHSL = this.rgbToHsl(rgb.r, rgb.g, rgb.b);
      }
    },
    updateFromHSL(type) {
      const hsl = type === 'foreground' ? this.foregroundHSL : this.backgroundHSL;
      const rgb = this.hslToRgb(hsl.h, hsl.s, hsl.l);
      const hexColor = this.rgbToHex(rgb.r, rgb.g, rgb.b);
      
      if (type === 'foreground') {
        this.foregroundColor = hexColor;
        this.foregroundRGB = rgb;
      } else {
        this.backgroundColor = hexColor;
        this.backgroundRGB = rgb;
      }
    },
    swapColors() {
      // Swap foreground and background colors
      const tempColor = this.foregroundColor;
      const tempRGB = { ...this.foregroundRGB };
      const tempHSL = { ...this.foregroundHSL };
      
      this.foregroundColor = this.backgroundColor;
      this.foregroundRGB = { ...this.backgroundRGB };
      this.foregroundHSL = { ...this.backgroundHSL };
      
      this.backgroundColor = tempColor;
      this.backgroundRGB = tempRGB;
      this.backgroundHSL = tempHSL;
    },
    saveCombo() {
      const newCombo = {
        foreground: this.foregroundColor,
        background: this.backgroundColor,
        ratio: this.contrastRatio,
        passesAA: this.isAANormalText
      };
      
      this.savedCombos.push(newCombo);
      localStorage.setItem('savedContrastCombos', JSON.stringify(this.savedCombos));
    },
    loadCombo(combo) {
      this.foregroundColor = combo.foreground;
      this.backgroundColor = combo.background;
      
      // Update RGB and HSL values
      this.updateColorFormats('foreground');
      this.updateColorFormats('background');
    },
    removeCombo(index) {
      this.savedCombos.splice(index, 1);
      localStorage.setItem('savedContrastCombos', JSON.stringify(this.savedCombos));
    }
  }
}
</script>

<style scoped>
.contrast-checker-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

h1, h2, h3 {
  color: #333;
}

h1 {
  text-align: center;
  margin-bottom: 10px;
}

.instructions {
  text-align: center;
  color: #666;
  margin-bottom: 30px;
}

.checker-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-bottom: 40px;
}

/* Color Input Styles */
.color-inputs {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.color-input-group {
  background-color: white;
  border-radius: 8px;
  padding: 15px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.input-row {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.color-picker {
  width: 50px;
  height: 50px;
  border: none;
  border-radius: 4px;
  background: none;
  cursor: pointer;
  margin-right: 15px;
}

.color-text-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: monospace;
  font-size: 16px;
}

.color-format-toggles {
  display: flex;
  margin: 10px 0;
}

.color-format-toggles button {
  flex: 1;
  padding: 8px;
  background-color: #f0f0f0;
  border: 1px solid #ddd;
  cursor: pointer;
}

.color-format-toggles button:first-child {
  border-radius: 4px 0 0 4px;
}

.color-format-toggles button:last-child {
  border-radius: 0 4px 4px 0;
}

.color-format-toggles button.active {
  background-color: #2196f3;
  color: white;
  border-color: #2196f3;
}

.slider-controls {
  margin-top: 15px;
}

.slider-controls label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

.slider-controls input {
  width: 100%;
  margin-top: 5px;
}

.swap-colors {
  display: flex;
  justify-content: center;
}

.swap-btn {
  background-color: #6200ea;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.swap-btn:hover {
  background-color: #5000c9;
}

/* Preview Styles */
.preview-section {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.preview-box {
  flex: 1;
  border-radius: 8px;
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  min-height: 200px;
}

.preview-text {
  text-align: center;
}

.large-text {
  font-size: 24px;
  margin: 10px 0;
}

.normal-text {
  font-size: 16px;
  margin: 10px 0;
}

.contrast-results {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.contrast-ratio {
  text-align: center;
}

.ratio-display {
  font-size: 32px;
  font-weight: bold;
  padding: 10px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.wcag-results {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.compliance-item {
  display: flex;
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.level {
  background-color: #333;
  color: white;
  padding: 15px;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 60px;
}

.compliance-details {
  flex: 1;
  padding: 10px 15px;
}

.pass, .fail {
  margin: 5px 0;
  padding: 5px 0;
}

.pass {
  color: #2e7d32;
}

.fail {
  color: #c62828;
}

.status-icon {
  font-weight: bold;
  margin-right: 5px;
}

/* Saved Combinations Styles */
.saved-combos {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-top: 30px;
}

.saved-combos h2 {
  margin-top: 0;
  margin-bottom: 20px;
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
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.save-btn:hover {
  background-color: #0d87e9;
}

.no-saved {
  text-align: center;
  color: #666;
  font-style: italic;
  padding: 20px;
}

.combos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 15px;
}

.saved-combo {
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  transition: transform 0.2s;
}

.saved-combo:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 10px rgba(0,0,0,0.15);
}

.combo-preview {
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.combo-text {
  font-size: 36px;
  font-weight: bold;
}

.combo-details {
  padding: 15px;
}

.combo-colors {
  margin-bottom: 10px;
}

.combo-color {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

.color-label {
  font-weight: bold;
}

.combo-ratio {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}

.ratio-value {
  font-weight: bold;
}

.combo-compliance {
  padding: 2px 8px;
  border-radius: 10px;
  font-size: 12px;
}

.combo-compliance.pass {
  background-color: #e8f5e9;
}

.combo-compliance:not(.pass) {
  background-color: #ffebee;
}

.combo-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.combo-actions button {
  flex: 1;
  padding: 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
  margin: 0 5px;
}

.combo-actions button:first-child {
  background-color: #2196f3;
  color: white;
}

.combo-actions button.remove-btn {
  background-color: #f44336;
  color: white;
}

/* Responsive Styles */
@media (max-width: 768px) {
  .checker-grid {
    grid-template-columns: 1fr;
  }
  
  .combos-grid {
    grid-template-columns: 1fr;
  }
}
</style>