<template>
  <div class="typography-pairing-container">
    <h1>Typography Pairing</h1>
    <p class="instructions">Discover beautiful font combinations for your website or brand</p>
    
    <div class="pairing-tools">
      <div class="filter-controls">
        <div class="pairing-style">
          <label for="pairingStyle">Pairing Style:</label>
          <select id="pairingStyle" v-model="pairingStyle" @change="updatePairings">
            <option value="classic">Classic</option>
            <option value="modern">Modern</option>
            <option value="creative">Creative</option>
            <option value="minimal">Minimal</option>
            <option value="elegant">Elegant</option>
          </select>
        </div>
        <div class="use-case">
          <label for="useCase">Use Case:</label>
          <select id="useCase" v-model="useCase" @change="updatePairings">
            <option value="business">Business/Corporate</option>
            <option value="blog">Blog/Magazine</option>
            <option value="portfolio">Portfolio/Creative</option>
            <option value="ecommerce">E-commerce</option>
            <option value="tech">Technology</option>
          </select>
        </div>
        <button class="refresh-btn" @click="randomizePairings">
          Randomize Pairings
        </button>
      </div>
    </div>
    
    <div class="pairing-grid">
      <div 
        v-for="(pairing, index) in filteredPairings" 
        :key="index" 
        class="pairing-card"
      >
        <div class="pairing-preview">
          <h2 :style="{ fontFamily: pairing.heading }">{{ pairing.heading }}</h2>
          <p :style="{ fontFamily: pairing.body }">
            {{ pairing.body }} works beautifully with this heading font. The combination creates 
            a {{ pairing.style }} feel that's perfect for {{ pairing.useCase }} websites.
          </p>
        </div>
        <div class="pairing-info">
          <div class="font-details">
            <div class="heading-font">
              <h4>Heading Font</h4>
              <code>font-family: {{ pairing.heading }};</code>
            </div>
            <div class="body-font">
              <h4>Body Font</h4>
              <code>font-family: {{ pairing.body }};</code>
            </div>
          </div>
          <div class="pairing-tags">
            <span class="tag style-tag">{{ pairing.style }}</span>
            <span class="tag use-case-tag">{{ pairing.useCase }}</span>
          </div>
          <button class="save-pairing-btn" @click="savePairing(pairing)">Save This Pairing</button>
        </div>
      </div>
    </div>
    
    <div v-if="filteredPairings.length === 0" class="no-results">
      <p>No typography pairings match your current filters. Try changing your selections.</p>
    </div>
    
    <div class="saved-pairings" v-if="savedPairings.length > 0">
      <h2>Your Saved Pairings</h2>
      <div class="saved-pairings-grid">
        <div 
          v-for="(pairing, index) in savedPairings" 
          :key="'saved-'+index" 
          class="saved-pairing-card"
        >
          <div class="saved-preview">
            <h3 :style="{ fontFamily: pairing.heading }">{{ pairing.heading }}</h3>
            <p :style="{ fontFamily: pairing.body }">{{ pairing.body }}</p>
          </div>
          <div class="saved-actions">
            <button class="remove-btn" @click="removeSavedPairing(index)">Remove</button>
            <button class="copy-btn" @click="copyPairingCSS(pairing)">Copy CSS</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TypographyPairing',
  data() {
    return {
      pairingStyle: 'classic',
      useCase: 'business',
      savedPairings: [],
      allPairings: [
        // Classic pairings
        {
          heading: 'Georgia, serif',
          body: 'Arial, sans-serif',
          style: 'classic',
          useCase: 'business'
        },
        {
          heading: 'Baskerville, serif',
          body: 'Helvetica, sans-serif',
          style: 'classic',
          useCase: 'business'
        },
        {
          heading: 'Times New Roman, serif',
          body: 'Tahoma, sans-serif',
          style: 'classic',
          useCase: 'blog'
        },
        {
          heading: 'Palatino, serif',
          body: 'Verdana, sans-serif',
          style: 'classic',
          useCase: 'portfolio'
        },
        
        // Modern pairings
        {
          heading: 'Helvetica, sans-serif',
          body: 'Garamond, serif',
          style: 'modern',
          useCase: 'tech'
        },
        {
          heading: 'Arial, sans-serif',
          body: 'Georgia, serif',
          style: 'modern',
          useCase: 'business'
        },
        {
          heading: 'Tahoma, sans-serif',
          body: 'Trebuchet MS, sans-serif',
          style: 'modern',
          useCase: 'ecommerce'
        },
        {
          heading: 'Calibri, sans-serif',
          body: 'Cambria, serif',
          style: 'modern',
          useCase: 'tech'
        },
        
        // Creative pairings
        {
          heading: 'Impact, sans-serif',
          body: 'Georgia, serif',
          style: 'creative',
          useCase: 'portfolio'
        },
        {
          heading: 'Comic Sans MS, cursive',
          body: 'Verdana, sans-serif',
          style: 'creative',
          useCase: 'blog'
        },
        {
          heading: 'Brush Script MT, cursive',
          body: 'Tahoma, sans-serif',
          style: 'creative',
          useCase: 'portfolio'
        },
        {
          heading: 'Copperplate, fantasy',
          body: 'Trebuchet MS, sans-serif',
          style: 'creative',
          useCase: 'portfolio'
        },
        
        // Minimal pairings
        {
          heading: 'Arial, sans-serif',
          body: 'Arial, sans-serif',
          style: 'minimal',
          useCase: 'tech'
        },
        {
          heading: 'Helvetica, sans-serif',
          body: 'Helvetica, sans-serif',
          style: 'minimal',
          useCase: 'business'
        },
        {
          heading: 'Verdana, sans-serif',
          body: 'Verdana, sans-serif',
          style: 'minimal',
          useCase: 'ecommerce'
        },
        {
          heading: 'Trebuchet MS, sans-serif',
          body: 'Tahoma, sans-serif',
          style: 'minimal',
          useCase: 'tech'
        },
        
        // Elegant pairings
        {
          heading: 'Didot, serif',
          body: 'Garamond, serif',
          style: 'elegant',
          useCase: 'portfolio'
        },
        {
          heading: 'Baskerville, serif',
          body: 'Palatino, serif',
          style: 'elegant',
          useCase: 'blog'
        },
        {
          heading: 'Garamond, serif',
          body: 'Georgia, serif',
          style: 'elegant',
          useCase: 'business'
        },
        {
          heading: 'Bodoni MT, serif',
          body: 'Cambria, serif',
          style: 'elegant',
          useCase: 'ecommerce'
        }
      ]
    }
  },
  computed: {
    filteredPairings() {
      return this.allPairings.filter(pairing => {
        const styleMatch = this.pairingStyle === 'all' || pairing.style === this.pairingStyle;
        const useCaseMatch = this.useCase === 'all' || pairing.useCase === this.useCase;
        return styleMatch && useCaseMatch;
      });
    }
  },
  mounted() {
    // Load saved pairings from localStorage if available
    const savedPairings = localStorage.getItem('savedTypographyPairings');
    if (savedPairings) {
      this.savedPairings = JSON.parse(savedPairings);
    }
  },
  methods: {
    updatePairings() {
      // This method exists to allow for future enhancements
      // like fetching pairings from an API
    },
    randomizePairings() {
      // Randomly change the filters to see different combinations
      const styles = ['classic', 'modern', 'creative', 'minimal', 'elegant'];
      const useCases = ['business', 'blog', 'portfolio', 'ecommerce', 'tech'];
      
      this.pairingStyle = styles[Math.floor(Math.random() * styles.length)];
      this.useCase = useCases[Math.floor(Math.random() * useCases.length)];
    },
    savePairing(pairing) {
      // Check if this pairing is already saved to avoid duplicates
      const isDuplicate = this.savedPairings.some(p => 
        p.heading === pairing.heading && p.body === pairing.body
      );
      
      if (!isDuplicate) {
        this.savedPairings.push({ ...pairing });
        localStorage.setItem('savedTypographyPairings', JSON.stringify(this.savedPairings));
      } else {
        alert('This pairing is already in your saved collection.');
      }
    },
    removeSavedPairing(index) {
      this.savedPairings.splice(index, 1);
      localStorage.setItem('savedTypographyPairings', JSON.stringify(this.savedPairings));
    },
    copyPairingCSS(pairing) {
      const css = `/* Typography */
h1, h2, h3, h4, h5, h6 {
  font-family: ${pairing.heading};
}

body, p, div, span, input, button, textarea {
  font-family: ${pairing.body};
}`;
      
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
.typography-pairing-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
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

.pairing-tools {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 30px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.filter-controls {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  align-items: center;
  justify-content: center;
}

.pairing-style, .use-case {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.pairing-style label, .use-case label {
  font-weight: bold;
  font-size: 14px;
}

.pairing-style select, .use-case select {
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ddd;
  min-width: 200px;
  font-size: 16px;
}

.refresh-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.refresh-btn:hover {
  background-color: #45a049;
}

.pairing-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
  gap: 30px;
  margin-bottom: 40px;
}

.pairing-card {
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
}

.pairing-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
}

.pairing-preview {
  padding: 30px;
  border-bottom: 1px solid #eee;
}

.pairing-preview h2 {
  margin-top: 0;
  margin-bottom: 15px;
  font-size: 28px;
  line-height: 1.2;
}

.pairing-preview p {
  margin: 0;
  line-height: 1.6;
  font-size: 16px;
}

.pairing-info {
  padding: 20px;
  background-color: #f9f9f9;
}

.font-details {
  display: flex;
  gap: 20px;
  margin-bottom: 15px;
}

.heading-font, .body-font {
  flex: 1;
}

.heading-font h4, .body-font h4 {
  margin-top: 0;
  margin-bottom: 5px;
  font-size: 14px;
  color: #666;
}

code {
  display: block;
  background-color: #f1f1f1;
  padding: 8px;
  border-radius: 4px;
  font-family: monospace;
  font-size: 12px;
  color: #333;
  word-break: break-all;
}

.pairing-tags {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}

.tag {
  display: inline-block;
  padding: 4px 8px;
  border-radius: 20px;
  font-size: 12px;
  color: white;
}

.style-tag {
  background-color: #2196f3;
}

.use-case-tag {
  background-color: #ff9800;
}

.save-pairing-btn {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 4px;
  background-color: #673ab7;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
}

.save-pairing-btn:hover {
  background-color: #5e35b1;
}

.no-results {
  background-color: #f5f5f5;
  padding: 30px;
  text-align: center;
  border-radius: 8px;
  margin-bottom: 30px;
}

.saved-pairings {
  margin-top: 50px;
}

.saved-pairings h2 {
  text-align: center;
  margin-bottom: 20px;
}

.saved-pairings-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}

.saved-pairing-card {
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.saved-preview {
  padding: 20px;
  border-bottom: 1px solid #eee;
}

.saved-preview h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 22px;
}

.saved-preview p {
  margin: 0;
  font-size: 14px;
}

.saved-actions {
  display: flex;
  padding: 10px;
  gap: 10px;
}

.saved-actions button {
  flex: 1;
  padding: 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.remove-btn {
  background-color: #f44336;
  color: white;
}

.copy-btn {
  background-color: #2196f3;
  color: white;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .pairing-grid {
    grid-template-columns: 1fr;
  }
  
  .font-details {
    flex-direction: column;
    gap: 10px;
  }
}
</style>