<template>
  <div class="font-explorer-container">
    <h1>Standard Font Explorer</h1>
    <p class="instructions">Select fonts from the list to preview them with different text samples</p>
    
    <div class="explorer-grid">
      <!-- Font selection sidebar -->
      <div class="font-selector">
        <h2>Available Fonts</h2>
        <div class="font-categories">
          <div class="category">
            <h3>Serif Fonts</h3>
            <ul class="font-list">
              <li v-for="font in serifFonts" :key="font" 
                  @click="selectFont(font)" 
                  :class="{ active: selectedFont === font }">
                <span class="font-name">{{ font }}</span>
              </li>
            </ul>
          </div>
          
          <div class="category">
            <h3>Sans-Serif Fonts</h3>
            <ul class="font-list">
              <li v-for="font in sansSerifFonts" :key="font" 
                  @click="selectFont(font)" 
                  :class="{ active: selectedFont === font }">
                <span class="font-name">{{ font }}</span>
              </li>
            </ul>
          </div>
          
          <div class="category">
            <h3>Monospace Fonts</h3>
            <ul class="font-list">
              <li v-for="font in monospaceFonts" :key="font" 
                  @click="selectFont(font)" 
                  :class="{ active: selectedFont === font }">
                <span class="font-name">{{ font }}</span>
              </li>
            </ul>
          </div>
          
          <div class="category">
            <h3>Display & Decorative</h3>
            <ul class="font-list">
              <li v-for="font in displayFonts" :key="font" 
                  @click="selectFont(font)" 
                  :class="{ active: selectedFont === font }">
                <span class="font-name">{{ font }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
      
      <!-- Font preview area -->
      <div class="font-preview">
        <div class="preview-header">
          <h2>Preview: <span class="current-font">{{ selectedFont }}</span></h2>
          <div class="preview-controls">
            <div class="size-control">
              <label for="fontSize">Size: {{ fontSize }}px</label>
              <input type="range" id="fontSize" v-model="fontSize" min="8" max="72" step="1">
            </div>
            <div class="weight-control">
              <label for="fontWeight">Weight:</label>
              <select id="fontWeight" v-model="fontWeight">
                <option value="100">Thin (100)</option>
                <option value="200">Extra Light (200)</option>
                <option value="300">Light (300)</option>
                <option value="400">Regular (400)</option>
                <option value="500">Medium (500)</option>
                <option value="600">Semi Bold (600)</option>
                <option value="700">Bold (700)</option>
                <option value="800">Extra Bold (800)</option>
                <option value="900">Black (900)</option>
              </select>
            </div>
            <div class="style-control">
              <label for="fontStyle">Style:</label>
              <select id="fontStyle" v-model="fontStyle">
                <option value="normal">Normal</option>
                <option value="italic">Italic</option>
              </select>
            </div>
          </div>
        </div>
        
        <div class="preview-content" :style="previewStyle">
          <div class="preview-section">
            <h3 class="preview-heading">Headings</h3>
            <h1>Heading Level 1</h1>
            <h2>Heading Level 2</h2>
            <h3>Heading Level 3</h3>
            <h4>Heading Level 4</h4>
          </div>
          
          <div class="preview-section">
            <h3 class="preview-heading">Paragraph Text</h3>
            <p>This is a paragraph showing how the font looks in a body of text. Good typography is essential for effective visual communication and user experience. The right font can establish mood, convey information clearly, and create visual hierarchy.</p>
            <p>Typography is the art and technique of arranging type to make written language legible, readable, and appealing when displayed. The arrangement of type involves selecting typefaces, point sizes, line lengths, line-spacing, and letter-spacing.</p>
          </div>
          
          <div class="preview-section">
            <h3 class="preview-heading">Special Characters</h3>
            <p class="special-chars">
              1234567890<br>
              !@#$%^&*()_+-=[]{}|;:'",./&lt;&gt;?<br>
              ABCDEFGHIJKLMNOPQRSTUVWXYZ<br>
              abcdefghijklmnopqrstuvwxyz
            </p>
          </div>
          
          <div class="preview-section">
            <h3 class="preview-heading">Custom Text</h3>
            <textarea 
              v-model="customText"
              placeholder="Type your custom text here to preview it in the selected font..."
              rows="4"
            ></textarea>
          </div>
        </div>
        
        <div class="font-info">
          <h3>Font Information</h3>
          <p><strong>Font Family:</strong> {{ selectedFont }}</p>
          <p><strong>Classification:</strong> {{ getFontClassification(selectedFont) }}</p>
          <p><strong>CSS Declaration:</strong></p>
          <code>font-family: {{ getCSSFontFamily(selectedFont) }};</code>
          <button @click="copyCSS" class="copy-btn">Copy CSS</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FontExplorer',
  data() {
    return {
      // Font collections
      serifFonts: [
        'Times New Roman', 'Georgia', 'Garamond', 'Baskerville', 'Cambria', 
        'Palatino', 'Bookman', 'Didot', 'Century Schoolbook', 'Bodoni MT'
      ],
      sansSerifFonts: [
        'Arial', 'Helvetica', 'Verdana', 'Tahoma', 'Trebuchet MS', 
        'Calibri', 'Century Gothic', 'Gill Sans', 'Segoe UI', 'Optima'
      ],
      monospaceFonts: [
        'Courier New', 'Courier', 'Lucida Console', 'Monaco', 'Consolas',
        'Liberation Mono', 'Menlo', 'Andale Mono', 'Letter Gothic', 'Bitstream Vera Sans Mono'
      ],
      displayFonts: [
        'Impact', 'Comic Sans MS', 'Papyrus', 'Brush Script MT', 'Copperplate',
        'Luminari', 'Chalkduster', 'Marker Felt', 'American Typewriter', 'Apple Chancery'
      ],
      
      // Currently selected properties
      selectedFont: 'Arial',
      fontSize: 16,
      fontWeight: '400',
      fontStyle: 'normal',
      customText: ''
    }
  },
  computed: {
    previewStyle() {
      return {
        fontFamily: `"${this.selectedFont}", sans-serif`,
        fontSize: `${this.fontSize}px`,
        fontWeight: this.fontWeight,
        fontStyle: this.fontStyle
      }
    }
  },
  methods: {
    selectFont(font) {
      this.selectedFont = font;
    },
    getFontClassification(font) {
      if (this.serifFonts.includes(font)) return 'Serif';
      if (this.sansSerifFonts.includes(font)) return 'Sans-Serif';
      if (this.monospaceFonts.includes(font)) return 'Monospace';
      if (this.displayFonts.includes(font)) return 'Display/Decorative';
      return 'Unknown';
    },
    getCSSFontFamily(font) {
      const classification = this.getFontClassification(font);
      const genericFamily = classification === 'Serif' ? 'serif' : 
                          classification === 'Sans-Serif' ? 'sans-serif' :
                          classification === 'Monospace' ? 'monospace' : 'sans-serif';
      
      return `"${font}", ${genericFamily}`;
    },
    copyCSS() {
      const css = `font-family: ${this.getCSSFontFamily(this.selectedFont)};`;
      navigator.clipboard.writeText(css).then(() => {
        alert('CSS copied to clipboard!');
      }).catch(err => {
        console.error('Could not copy text: ', err);
      });
    }
  }
}
</script>

<style scoped>
.font-explorer-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
  color: #333;
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

.explorer-grid {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 30px;
  margin-bottom: 40px;
}

/* Font selector sidebar */
.font-selector {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  height: fit-content;
  max-height: 700px;
  overflow-y: auto;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.font-categories {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.category h3 {
  font-size: 1.1rem;
  margin-bottom: 10px;
  padding-bottom: 5px;
  border-bottom: 1px solid #ddd;
}

.font-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.font-list li {
  padding: 8px 12px;
  margin-bottom: 5px;
  cursor: pointer;
  border-radius: 4px;
  transition: all 0.2s ease;
}

.font-list li:hover {
  background-color: #e9e9e9;
}

.font-list li.active {
  background-color: #2196f3;
  color: white;
}

.font-name {
  display: block;
  pointer-events: none;
}

/* Render each font name in its own font */
.font-list li:nth-child(1) .font-name { font-family: "Times New Roman", serif; }
.font-list li:nth-child(2) .font-name { font-family: Georgia, serif; }
.font-list li:nth-child(3) .font-name { font-family: Garamond, serif; }
.font-list li:nth-child(4) .font-name { font-family: Baskerville, serif; }
.font-list li:nth-child(5) .font-name { font-family: Cambria, serif; }
.font-list li:nth-child(6) .font-name { font-family: Palatino, serif; }
.font-list li:nth-child(7) .font-name { font-family: Bookman, serif; }
.font-list li:nth-child(8) .font-name { font-family: Didot, serif; }
.font-list li:nth-child(9) .font-name { font-family: "Century Schoolbook", serif; }
.font-list li:nth-child(10) .font-name { font-family: "Bodoni MT", serif; }

/* Font preview area */
.font-preview {
  background-color: white;
  border-radius: 8px;
  padding: 30px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.preview-header {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-bottom: 25px;
  padding-bottom: 15px;
  border-bottom: 1px solid #eee;
}

.current-font {
  color: #2196f3;
}

.preview-controls {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  align-items: center;
}

.size-control {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.size-control input[type="range"] {
  width: 200px;
}

.weight-control select, .style-control select {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ddd;
  font-size: 14px;
}

.preview-content {
  margin-bottom: 30px;
}

.preview-section {
  margin-bottom: 25px;
  padding-bottom: 20px;
  border-bottom: 1px solid #eee;
}

.preview-heading {
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #666;
  margin-bottom: 15px;
  font-family: system-ui, sans-serif !important;
}

.special-chars {
  line-height: 1.7;
}

textarea {
  width: 100%;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: inherit;
  line-height: 1.5;
  resize: vertical;
}

.font-info {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
}

.font-info h3 {
  margin-top: 0;
  margin-bottom: 15px;
}

.font-info p {
  margin: 10px 0;
}

code {
  display: block;
  background-color: #f1f1f1;
  padding: 12px;
  border-radius: 4px;
  font-family: monospace;
  margin: 10px 0;
}

.copy-btn {
  background-color: #2196f3;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.copy-btn:hover {
  background-color: #0d87e9;
}

/* Responsive styles */
@media (max-width: 900px) {
  .explorer-grid {
    grid-template-columns: 1fr;
  }
  
  .font-selector {
    max-height: 300px;
  }
}
</style>