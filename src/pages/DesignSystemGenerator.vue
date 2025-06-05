<template>
  <div class="design-system-container">
    <h1>Design System Generator</h1>
    <p class="instructions">Create a consistent design system for your brand or website</p>
    
    <!-- Main interface divided into sections -->
    <div class="design-system-grid">
      <!-- Navigation sidebar -->
      <div class="sidebar">
        <nav class="section-nav">
          <button 
            v-for="(section, index) in sections" 
            :key="index"
            :class="{ active: activeSection === section.id }"
            @click="activeSection = section.id"
          >
            {{ section.name }}
          </button>
        </nav>
        
        <div class="action-buttons">
          <button class="save-btn" @click="saveDesignSystem">Save Design System</button>
          <button class="export-btn" @click="exportDesignSystem">Export as CSS/JSON</button>
        </div>
      </div>
      
      <!-- Content area -->
      <div class="content-area">
        <!-- Color Palette Section -->
        <div v-show="activeSection === 'colors'" class="section colors-section">
          <h2>Color Palette</h2>
          <p class="section-desc">Define your brand's primary and secondary colors along with neutral shades.</p>
          
          <div class="color-groups">
            <!-- Primary Colors -->
            <div class="color-group">
              <h3>Primary Colors</h3>
              <p class="group-desc">Your main brand colors used for primary actions, links, and branded elements.</p>
              
              <div class="color-row">
                <div class="color-item main-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.primary }"
                    @click="activeColorPicker = 'primary'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Primary</div>
                    <div class="color-value">{{ designSystem.colors.primary }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'primary'"
                    type="color"
                    v-model="designSystem.colors.primary"
                    class="color-picker"
                    @change="generateShades('primary')"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div 
                  v-for="(shade, index) in designSystem.colors.primaryShades" 
                  :key="'primary-' + index"
                  class="color-item shade"
                >
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: shade.value }"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">{{ shade.name }}</div>
                    <div class="color-value">{{ shade.value }}</div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Secondary Colors -->
            <div class="color-group">
              <h3>Secondary Colors</h3>
              <p class="group-desc">Used for secondary actions, highlights, and supporting elements.</p>
              
              <div class="color-row">
                <div class="color-item main-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.secondary }"
                    @click="activeColorPicker = 'secondary'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Secondary</div>
                    <div class="color-value">{{ designSystem.colors.secondary }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'secondary'"
                    type="color"
                    v-model="designSystem.colors.secondary"
                    class="color-picker"
                    @change="generateShades('secondary')"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div 
                  v-for="(shade, index) in designSystem.colors.secondaryShades" 
                  :key="'secondary-' + index"
                  class="color-item shade"
                >
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: shade.value }"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">{{ shade.name }}</div>
                    <div class="color-value">{{ shade.value }}</div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Neutral Colors -->
            <div class="color-group">
              <h3>Neutral Colors</h3>
              <p class="group-desc">Used for text, backgrounds, borders, and other UI elements.</p>
              
              <div class="color-row">
                <div class="color-item main-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.neutral }"
                    @click="activeColorPicker = 'neutral'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Neutral</div>
                    <div class="color-value">{{ designSystem.colors.neutral }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'neutral'"
                    type="color"
                    v-model="designSystem.colors.neutral"
                    class="color-picker"
                    @change="generateShades('neutral')"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div 
                  v-for="(shade, index) in designSystem.colors.neutralShades" 
                  :key="'neutral-' + index"
                  class="color-item shade"
                >
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: shade.value }"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">{{ shade.name }}</div>
                    <div class="color-value">{{ shade.value }}</div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Accent/Semantic Colors -->
            <div class="color-group">
              <h3>Semantic Colors</h3>
              <p class="group-desc">Colors used for success, error, warning, and information states.</p>
              
              <div class="semantic-colors">
                <div class="color-item semantic-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.success }"
                    @click="activeColorPicker = 'success'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Success</div>
                    <div class="color-value">{{ designSystem.colors.success }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'success'"
                    type="color"
                    v-model="designSystem.colors.success"
                    class="color-picker"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div class="color-item semantic-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.error }"
                    @click="activeColorPicker = 'error'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Error</div>
                    <div class="color-value">{{ designSystem.colors.error }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'error'"
                    type="color"
                    v-model="designSystem.colors.error"
                    class="color-picker"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div class="color-item semantic-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.warning }"
                    @click="activeColorPicker = 'warning'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Warning</div>
                    <div class="color-value">{{ designSystem.colors.warning }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'warning'"
                    type="color"
                    v-model="designSystem.colors.warning"
                    class="color-picker"
                    @blur="activeColorPicker = null"
                  />
                </div>
                
                <div class="color-item semantic-color">
                  <div 
                    class="color-preview" 
                    :style="{ backgroundColor: designSystem.colors.info }"
                    @click="activeColorPicker = 'info'"
                  ></div>
                  <div class="color-info">
                    <div class="color-label">Info</div>
                    <div class="color-value">{{ designSystem.colors.info }}</div>
                  </div>
                  <input 
                    v-if="activeColorPicker === 'info'"
                    type="color"
                    v-model="designSystem.colors.info"
                    class="color-picker"
                    @blur="activeColorPicker = null"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Typography Section -->
        <div v-show="activeSection === 'typography'" class="section typography-section">
          <h2>Typography</h2>
          <p class="section-desc">Define your font styles for headings, body text, and UI elements.</p>
          
          <div class="typography-settings">
            <!-- Font Family Selection -->
            <div class="settings-group">
              <h3>Font Families</h3>
              <div class="font-families">
                <div class="font-family-item">
                  <label>Heading Font</label>
                  <select v-model="designSystem.typography.headingFont" @change="updateTypographyPreview">
                    <option v-for="font in availableFonts" :key="font" :value="font">{{ font }}</option>
                  </select>
                  <div class="font-preview" :style="{ fontFamily: designSystem.typography.headingFont }">
                    Aa Bb Cc Xx Yy Zz 123
                  </div>
                </div>
                
                <div class="font-family-item">
                  <label>Body Font</label>
                  <select v-model="designSystem.typography.bodyFont" @change="updateTypographyPreview">
                    <option v-for="font in availableFonts" :key="font" :value="font">{{ font }}</option>
                  </select>
                  <div class="font-preview" :style="{ fontFamily: designSystem.typography.bodyFont }">
                    Aa Bb Cc Xx Yy Zz 123
                  </div>
                </div>
                
                <div class="font-family-item">
                  <label>UI Font</label>
                  <select v-model="designSystem.typography.uiFont" @change="updateTypographyPreview">
                    <option v-for="font in availableFonts" :key="font" :value="font">{{ font }}</option>
                  </select>
                  <div class="font-preview" :style="{ fontFamily: designSystem.typography.uiFont }">
                    Aa Bb Cc Xx Yy Zz 123
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Base Text Size -->
            <div class="settings-group">
              <h3>Base Text Size</h3>
              <p class="settings-desc">This is the base size for paragraph text. All other text sizes are calculated from this.</p>
              
              <div class="size-selector">
                <label>Base Size: {{ designSystem.typography.baseSize }}px</label>
                <input 
                  type="range" 
                  v-model.number="designSystem.typography.baseSize" 
                  min="14" 
                  max="22" 
                  step="1"
                  @input="updateTypographyPreview"
                >
                <div class="size-range">
                  <span>14px</span>
                  <span>22px</span>
                </div>
              </div>
            </div>
            
            <!-- Type Scale -->
            <div class="settings-group">
              <h3>Type Scale</h3>
              <p class="settings-desc">The ratio between text sizes in your typographic hierarchy.</p>
              
              <div class="scale-selector">
                <label>Scale Ratio:</label>
                <select v-model="designSystem.typography.scaleRatio" @change="updateTypographyPreview">
                  <option value="1.067">Minor Second (1.067)</option>
                  <option value="1.125">Major Second (1.125)</option>
                  <option value="1.200">Minor Third (1.200)</option>
                  <option value="1.250">Major Third (1.250)</option>
                  <option value="1.333">Perfect Fourth (1.333)</option>
                  <option value="1.414">Augmented Fourth (1.414)</option>
                  <option value="1.500">Perfect Fifth (1.500)</option>
                  <option value="1.618">Golden Ratio (1.618)</option>
                </select>
              </div>
            </div>
            
            <!-- Line Height -->
            <div class="settings-group">
              <h3>Line Heights</h3>
              
              <div class="line-height-settings">
                <div class="line-height-item">
                  <label>Headings: {{ designSystem.typography.headingLineHeight }}</label>
                  <input 
                    type="range" 
                    v-model.number="designSystem.typography.headingLineHeight" 
                    min="1" 
                    max="2" 
                    step="0.05"
                    @input="updateTypographyPreview"
                  >
                  <div class="size-range">
                    <span>1</span>
                    <span>2</span>
                  </div>
                </div>
                
                <div class="line-height-item">
                  <label>Body: {{ designSystem.typography.bodyLineHeight }}</label>
                  <input 
                    type="range" 
                    v-model.number="designSystem.typography.bodyLineHeight" 
                    min="1" 
                    max="2" 
                    step="0.05"
                    @input="updateTypographyPreview"
                  >
                  <div class="size-range">
                    <span>1</span>
                    <span>2</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Typography Preview -->
          <div class="typography-preview">
            <h3 class="preview-title">Typography Preview</h3>
            
            <div class="type-preview-content">
              <h1 :style="headingPreviewStyle('h1')">Heading 1 ({{ calculatedSizes.h1 }}px)</h1>
              <h2 :style="headingPreviewStyle('h2')">Heading 2 ({{ calculatedSizes.h2 }}px)</h2>
              <h3 :style="headingPreviewStyle('h3')">Heading 3 ({{ calculatedSizes.h3 }}px)</h3>
              <h4 :style="headingPreviewStyle('h4')">Heading 4 ({{ calculatedSizes.h4 }}px)</h4>
              <h5 :style="headingPreviewStyle('h5')">Heading 5 ({{ calculatedSizes.h5 }}px)</h5>
              <h6 :style="headingPreviewStyle('h6')">Heading 6 ({{ calculatedSizes.h6 }}px)</h6>
              
              <div class="text-sample" :style="bodyPreviewStyle()">
                <p class="large" :style="{fontSize: calculatedSizes.large + 'px'}">
                  Large Paragraph ({{ calculatedSizes.large }}px): The quick brown fox jumps over the lazy dog.
                </p>
                
                <p>
                  Base Paragraph ({{ designSystem.typography.baseSize }}px): Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                  Donec a diam lectus. Sed sit amet ipsum mauris. Maecenas congue ligula ac quam viverra nec consectetur ante hendrerit.
                </p>
                
                <p class="small" :style="{fontSize: calculatedSizes.small + 'px'}">
                  Small Text ({{ calculatedSizes.small }}px): This is smaller text often used for captions or supporting information.
                </p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Spacing Section -->
        <div v-show="activeSection === 'spacing'" class="section spacing-section">
          <h2>Spacing System</h2>
          <p class="section-desc">Create a consistent spacing scale for margins, padding and layout.</p>
          
          <div class="spacing-settings">
            <!-- Base Unit -->
            <div class="settings-group">
              <h3>Base Spacing Unit</h3>
              <p class="settings-desc">All spacing values will be calculated as multiples of this base unit.</p>
              
              <div class="base-unit-control">
                <label>Base Unit: {{ designSystem.spacing.baseUnit }}px</label>
                <input 
                  type="range" 
                  v-model.number="designSystem.spacing.baseUnit" 
                  min="4" 
                  max="16" 
                  step="1"
                  @input="updateSpacingScale"
                >
                <div class="size-range">
                  <span>4px</span>
                  <span>16px</span>
                </div>
              </div>
            </div>
            
            <!-- Spacing Scale Type -->
            <div class="settings-group">
              <h3>Scale Type</h3>
              <div class="scale-type-control">
                <div class="scale-option" :class="{ active: designSystem.spacing.scaleType === 'linear' }">
                  <input 
                    type="radio" 
                    id="linearScale" 
                    value="linear" 
                    v-model="designSystem.spacing.scaleType"
                    @change="updateSpacingScale"
                  >
                  <label for="linearScale">Linear Scale</label>
                  <p class="option-desc">Even spacing increments (e.g., 4px, 8px, 12px, 16px)</p>
                </div>
                
                <div class="scale-option" :class="{ active: designSystem.spacing.scaleType === 'geometric' }">
                  <input 
                    type="radio" 
                    id="geometricScale" 
                    value="geometric" 
                    v-model="designSystem.spacing.scaleType"
                    @change="updateSpacingScale"
                  >
                  <label for="geometricScale">Geometric Scale</label>
                  <p class="option-desc">Multiplying increments (e.g., 4px, 8px, 16px, 32px)</p>
                </div>
              </div>
            </div>
            
            <!-- Scale Factor (for geometric scale) -->
            <div v-if="designSystem.spacing.scaleType === 'geometric'" class="settings-group">
              <h3>Scale Factor</h3>
              <p class="settings-desc">The multiplier used between consecutive spacing values.</p>
              
              <div class="factor-control">
                <label>Factor: {{ designSystem.spacing.scaleFactor }}x</label>
                <select 
                  v-model.number="designSystem.spacing.scaleFactor"
                  @change="updateSpacingScale"
                >
                  <option :value="1.5">1.5x</option>
                  <option :value="2">2x (Double)</option>
                  <option :value="3">3x (Triple)</option>
                </select>
              </div>
            </div>
            
            <!-- Number of Spacing Levels -->
            <div class="settings-group">
              <h3>Spacing Levels</h3>
              <p class="settings-desc">Number of spacing values in your scale.</p>
              
              <div class="levels-control">
                <label>Levels: {{ designSystem.spacing.levels }}</label>
                <input 
                  type="range" 
                  v-model.number="designSystem.spacing.levels" 
                  min="4" 
                  max="10" 
                  step="1"
                  @input="updateSpacingScale"
                >
                <div class="size-range">
                  <span>4</span>
                  <span>10</span>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Spacing Scale Preview -->
          <div class="spacing-preview">
            <h3>Spacing Scale Preview</h3>
            
            <div class="spacing-scale">
              <div 
                v-for="(space, index) in designSystem.spacing.values" 
                :key="'space-' + index"
                class="spacing-item"
              >
                <div class="spacing-visual">
                  <div class="spacing-bar" :style="{ width: space.value + 'px' }"></div>
                </div>
                <div class="spacing-info">
                  <div class="spacing-name">{{ space.name }}</div>
                  <div class="spacing-value">{{ space.value }}px</div>
                </div>
              </div>
            </div>
            
            <div class="spacing-examples">
              <h3>Example Applications</h3>
              
              <div class="examples-grid">
                <!-- Margins Example -->
                <div class="example-card">
                  <h4>Margins</h4>
                  <div class="example-container">
                    <div 
                      class="example-box margin-example" 
                      :style="{ margin: designSystem.spacing.values[2]?.value + 'px' }"
                    >
                      Element with margins
                    </div>
                  </div>
                  <div class="example-code">margin: {{ designSystem.spacing.values[2]?.value }}px;</div>
                </div>
                
                <!-- Padding Example -->
                <div class="example-card">
                  <h4>Padding</h4>
                  <div class="example-container">
                    <div 
                      class="example-box padding-example" 
                      :style="{ padding: designSystem.spacing.values[1]?.value + 'px' }"
                    >
                      Element with padding
                    </div>
                  </div>
                  <div class="example-code">padding: {{ designSystem.spacing.values[1]?.value }}px;</div>
                </div>
                
                <!-- Gap Example -->
                <div class="example-card">
                  <h4>Gap (Flexbox/Grid)</h4>
                  <div class="example-container">
                    <div 
                      class="example-flex"
                      :style="{ gap: designSystem.spacing.values[1]?.value + 'px' }"
                    >
                      <div class="flex-item">1</div>
                      <div class="flex-item">2</div>
                      <div class="flex-item">3</div>
                    </div>
                  </div>
                  <div class="example-code">gap: {{ designSystem.spacing.values[1]?.value }}px;</div>
                </div>
                
                <!-- Layout Example -->
                <div class="example-card">
                  <h4>Layout Spacing</h4>
                  <div class="example-container">
                    <div class="layout-example">
                      <div class="layout-header">Header</div>
                      <div 
                        class="layout-content" 
                        :style="{ marginTop: designSystem.spacing.values[3]?.value + 'px' }"
                      >
                        Content
                      </div>
                      <div 
                        class="layout-footer"
                        :style="{ marginTop: designSystem.spacing.values[3]?.value + 'px' }"
                      >
                        Footer
                      </div>
                    </div>
                  </div>
                  <div class="example-code">margin-top: {{ designSystem.spacing.values[3]?.value }}px;</div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Components Section -->
        <div v-show="activeSection === 'components'" class="section components-section">
          <h2>Component Styles</h2>
          <p class="section-desc">Preview how basic UI components look with your design system.</p>
          
          <div class="components-preview">
            <div class="component-row">
              <!-- Buttons -->
              <div class="component-group">
                <h3>Buttons</h3>
                <div class="component-samples">
                  <button 
                    class="ds-button ds-primary" 
                    :style="{
                      backgroundColor: designSystem.colors.primary,
                      color: '#ffffff',
                      fontFamily: designSystem.typography.uiFont,
                      padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[1]?.value}px`
                    }"
                  >
                    Primary Button
                  </button>
                  
                  <button 
                    class="ds-button ds-secondary" 
                    :style="{
                      backgroundColor: designSystem.colors.secondary,
                      color: '#ffffff',
                      fontFamily: designSystem.typography.uiFont,
                      padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[1]?.value}px`
                    }"
                  >
                    Secondary Button
                  </button>
                  
                  <button 
                    class="ds-button ds-outlined" 
                    :style="{
                      backgroundColor: 'transparent',
                      color: designSystem.colors.primary,
                      borderColor: designSystem.colors.primary,
                      fontFamily: designSystem.typography.uiFont,
                      padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[1]?.value}px`
                    }"
                  >
                    Outlined Button
                  </button>
                  
                  <button 
                    class="ds-button ds-text" 
                    :style="{
                      backgroundColor: 'transparent',
                      color: designSystem.colors.primary,
                      fontFamily: designSystem.typography.uiFont,
                      padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[1]?.value}px`
                    }"
                  >
                    Text Button
                  </button>
                </div>
              </div>
              
              <!-- Cards -->
              <div class="component-group">
                <h3>Cards</h3>
                <div class="component-samples">
                  <div 
                    class="ds-card" 
                    :style="{
                      backgroundColor: '#ffffff',
                      borderRadius: '8px',
                      boxShadow: '0 2px 8px rgba(0, 0, 0, 0.1)',
                      overflow: 'hidden'
                    }"
                  >
                    <div 
                      class="ds-card-header" 
                      :style="{
                        padding: `${designSystem.spacing.values[1]?.value}px`,
                        borderBottom: `1px solid ${designSystem.colors.neutralShades[0]?.value || '#f0f0f0'}`
                      }"
                    >
                      <h4 
                        :style="{
                          fontFamily: designSystem.typography.headingFont,
                          color: designSystem.colors.neutral,
                          margin: 0
                        }"
                      >
                        Card Title
                      </h4>
                    </div>
                    <div 
                      class="ds-card-content" 
                      :style="{
                        padding: `${designSystem.spacing.values[1]?.value}px`,
                        fontFamily: designSystem.typography.bodyFont,
                        fontSize: `${designSystem.typography.baseSize}px`
                      }"
                    >
                      <p :style="{ margin: 0 }">
                        This is a sample card component using your design system styles.
                      </p>
                    </div>
                    <div 
                      class="ds-card-actions" 
                      :style="{
                        display: 'flex',
                        justifyContent: 'flex-end',
                        padding: `${designSystem.spacing.values[0]?.value}px ${designSystem.spacing.values[1]?.value}px`,
                        gap: `${designSystem.spacing.values[0]?.value}px`
                      }"
                    >
                      <button 
                        class="ds-button ds-text" 
                        :style="{
                          backgroundColor: 'transparent',
                          color: designSystem.colors.primary,
                          fontFamily: designSystem.typography.uiFont,
                          padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[0]?.value}px`
                        }"
                      >
                        Cancel
                      </button>
                      <button 
                        class="ds-button ds-primary" 
                        :style="{
                          backgroundColor: designSystem.colors.primary,
                          color: '#ffffff',
                          fontFamily: designSystem.typography.uiFont,
                          padding: `${designSystem.spacing.values[0]?.value/2}px ${designSystem.spacing.values[0]?.value}px`
                        }"
                      >
                        Submit
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="component-row">
              <!-- Form Controls -->
              <div class="component-group">
                <h3>Form Controls</h3>
                <div class="component-samples">
                  <div class="ds-form-group">
                    <label 
                      :style="{
                        display: 'block',
                        marginBottom: `${designSystem.spacing.values[0]?.value/2}px`,
                        fontFamily: designSystem.typography.uiFont,
                        fontSize: `${designSystem.typography.baseSize*0.875}px`,
                        color: designSystem.colors.neutral
                      }"
                    >
                      Text Input
                    </label>
                    <input 
                      type="text" 
                      placeholder="Enter text"
                      :style="{
                        display: 'block',
                        width: '100%',
                        padding: `${designSystem.spacing.values[0]?.value}px`,
                        border: `1px solid ${designSystem.colors.neutralShades[1]?.value || '#ddd'}`,
                        borderRadius: '4px',
                        fontFamily: designSystem.typography.bodyFont,
                        fontSize: `${designSystem.typography.baseSize}px`
                      }"
                    />
                  </div>
                  
                  <div class="ds-form-group">
                    <label 
                      :style="{
                        display: 'block',
                        marginBottom: `${designSystem.spacing.values[0]?.value/2}px`,
                        fontFamily: designSystem.typography.uiFont,
                        fontSize: `${designSystem.typography.baseSize*0.875}px`,
                        color: designSystem.colors.neutral
                      }"
                    >
                      Select Input
                    </label>
                    <select 
                      :style="{
                        display: 'block',
                        width: '100%',
                        padding: `${designSystem.spacing.values[0]?.value}px`,
                        border: `1px solid ${designSystem.colors.neutralShades[1]?.value || '#ddd'}`,
                        borderRadius: '4px',
                        fontFamily: designSystem.typography.bodyFont,
                        fontSize: `${designSystem.typography.baseSize}px`
                      }"
                    >
                      <option>Option 1</option>
                      <option>Option 2</option>
                      <option>Option 3</option>
                    </select>
                  </div>
                  
                  <div class="ds-form-group">
                    <div 
                      class="ds-checkbox"
                      :style="{
                        display: 'flex',
                        alignItems: 'center',
                        gap: `${designSystem.spacing.values[0]?.value/2}px`,
                        fontFamily: designSystem.typography.bodyFont,
                        fontSize: `${designSystem.typography.baseSize}px`
                      }"
                    >
                      <input type="checkbox" id="checkbox" />
                      <label for="checkbox">Checkbox option</label>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Alerts -->
              <div class="component-group">
                <h3>Alerts</h3>
                <div class="component-samples">
                  <div 
                    class="ds-alert ds-success" 
                    :style="{
                      backgroundColor: `${designSystem.colors.success}22`,
                      color: designSystem.colors.success,
                      padding: `${designSystem.spacing.values[1]?.value}px`,
                      borderRadius: '4px',
                      border: `1px solid ${designSystem.colors.success}`,
                      fontFamily: designSystem.typography.bodyFont,
                      fontSize: `${designSystem.typography.baseSize}px`
                    }"
                  >
                    This is a success alert message.
                  </div>
                  
                  <div 
                    class="ds-alert ds-error" 
                    :style="{
                      backgroundColor: `${designSystem.colors.error}22`,
                      color: designSystem.colors.error,
                      padding: `${designSystem.spacing.values[1]?.value}px`,
                      borderRadius: '4px',
                      border: `1px solid ${designSystem.colors.error}`,
                      fontFamily: designSystem.typography.bodyFont,
                      fontSize: `${designSystem.typography.baseSize}px`
                    }"
                  >
                    This is an error alert message.
                  </div>
                  
                  <div 
                    class="ds-alert ds-warning" 
                    :style="{
                      backgroundColor: `${designSystem.colors.warning}22`,
                      color: designSystem.colors.warning,
                      padding: `${designSystem.spacing.values[1]?.value}px`,
                      borderRadius: '4px',
                      border: `1px solid ${designSystem.colors.warning}`,
                      fontFamily: designSystem.typography.bodyFont,
                      fontSize: `${designSystem.typography.baseSize}px`
                    }"
                  >
                    This is a warning alert message.
                  </div>
                  
                  <div 
                    class="ds-alert ds-info" 
                    :style="{
                      backgroundColor: `${designSystem.colors.info}22`,
                      color: designSystem.colors.info,
                      padding: `${designSystem.spacing.values[1]?.value}px`,
                      borderRadius: '4px',
                      border: `1px solid ${designSystem.colors.info}`,
                      fontFamily: designSystem.typography.bodyFont,
                      fontSize: `${designSystem.typography.baseSize}px`
                    }"
                  >
                    This is an information alert message.
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Navigation -->
            <div class="component-row">
              <div class="component-group full-width">
                <h3>Navigation</h3>
                <div class="component-samples">
                  <div 
                    class="ds-nav" 
                    :style="{
                      display: 'flex',
                      backgroundColor: designSystem.colors.primary,
                      color: '#ffffff',
                      padding: `${designSystem.spacing.values[0]?.value}px ${designSystem.spacing.values[1]?.value}px`,
                      fontFamily: designSystem.typography.uiFont
                    }"
                  >
                    <div 
                      class="ds-nav-brand" 
                      :style="{
                        fontWeight: 'bold',
                        fontSize: `${designSystem.typography.baseSize*1.25}px`,
                        marginRight: `${designSystem.spacing.values[2]?.value}px`,
                        display: 'flex',
                        alignItems: 'center'
                      }"
                    >
                      Brand
                    </div>
                    <div 
                      class="ds-nav-links" 
                      :style="{
                        display: 'flex',
                        gap: `${designSystem.spacing.values[1]?.value}px`,
                        alignItems: 'center'
                      }"
                    >
                      <a 
                        href="#" 
                        class="ds-nav-link active" 
                        :style="{
                          color: '#ffffff',
                          fontWeight: 'bold',
                          textDecoration: 'none'
                        }"
                      >
                        Home
                      </a>
                      <a 
                        href="#" 
                        class="ds-nav-link" 
                        :style="{
                          color: '#ffffffcc',
                          textDecoration: 'none'
                        }"
                      >
                        Features
                      </a>
                      <a 
                        href="#" 
                        class="ds-nav-link" 
                        :style="{
                          color: '#ffffffcc',
                          textDecoration: 'none'
                        }"
                      >
                        Pricing
                      </a>
                      <a 
                        href="#" 
                        class="ds-nav-link" 
                        :style="{
                          color: '#ffffffcc',
                          textDecoration: 'none'
                        }"
                      >
                        About
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Export Section -->
        <div v-show="activeSection === 'export'" class="section export-section">
          <h2>Export & Integration</h2>
          <p class="section-desc">Export your design system as CSS variables, SCSS, or JSON.</p>
          
          <div class="export-options">
            <div class="settings-group">
              <h3>Export Format</h3>
              <p class="settings-desc">Choose the format you want to export your design system in.</p>
              
              <div class="format-selector">
                <div 
                  v-for="format in exportFormats" 
                  :key="format.id"
                  class="format-option"
                  :class="{ active: selectedExportFormat === format.id }"
                  @click="selectedExportFormat = format.id"
                >
                  <div class="format-icon">{{ format.icon }}</div>
                  <div class="format-info">
                    <h4>{{ format.name }}</h4>
                    <p>{{ format.description }}</p>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="export-preview">
              <h3>Export Preview</h3>
              <pre class="code-preview"><code>{{ generateExportPreview() }}</code></pre>
              <div class="export-actions">
                <button class="copy-btn" @click="copyExportCode">Copy to Clipboard</button>
                <button class="download-btn" @click="downloadExportFile">Download File</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DesignSystemGenerator',
  data() {
    return {
      // Active section tracker
      activeSection: 'colors',
      
      // Navigation sections
      sections: [
        { id: 'colors', name: 'Color Palette' },
        { id: 'typography', name: 'Typography' },
        { id: 'spacing', name: 'Spacing' },
        { id: 'components', name: 'Components' },
        { id: 'export', name: 'Export' }
      ],
      
      // Design system data structure with default values
      designSystem: {
        colors: {
          primary: '#3f51b5',
          primaryShades: [],
          secondary: '#ff4081',
          secondaryShades: [],
          neutral: '#607d8b',
          neutralShades: [],
          success: '#4caf50',
          error: '#f44336',
          warning: '#ff9800',
          info: '#2196f3'
        },
        typography: {
          headingFont: 'Arial',
          bodyFont: 'Georgia',
          uiFont: 'Verdana',
          baseSize: 16,
          scaleRatio: 1.125,
          headingLineHeight: 1.2,
          bodyLineHeight: 1.5
        },
        spacing: {
          baseUnit: 8,
          scaleType: 'linear',
          scaleFactor: 2,
          levels: 5,
          values: []
        },
        components: {}
      },
      
      // Calculated font sizes
      calculatedSizes: {
        h1: 32,
        h2: 24,
        h3: 18.72,
        h4: 16,
        h5: 13.28,
        h6: 10.72,
        large: 18.72,
        small: 13.28
      },
      
      // Active color picker
      activeColorPicker: null,
      
      // Save state
      isSaved: false,
      lastSaved: null,
      
      // Available fonts for selection
      availableFonts: ['Arial', 'Verdana', 'Times New Roman', 'Georgia', 'Courier New', 'Brush Script MT'],
      
      // Export settings
      exportFormats: [
        { id: 'css', name: 'CSS Variables', description: 'Export your design system as CSS custom properties (variables).', icon: '🌈' },
        { id: 'scss', name: 'SCSS', description: 'Export your design system as SCSS variables and mixins.', icon: '💎' },
        { id: 'json', name: 'JSON', description: 'Export your design system as a JSON file.', icon: '📦' }
      ],
      selectedExportFormat: 'css'
    }
  },
  computed: {
    // Typography preview styles
    headingPreviewStyle() {
      return (level) => {
        return {
          fontFamily: this.designSystem.typography.headingFont,
          fontSize: `${this.calculatedSizes[level]}px`,
          lineHeight: this.designSystem.typography.headingLineHeight,
          marginBottom: '15px'
        };
      };
    },
    bodyPreviewStyle() {
      return () => {
        return {
          fontFamily: this.designSystem.typography.bodyFont,
          fontSize: `${this.designSystem.typography.baseSize}px`,
          lineHeight: this.designSystem.typography.bodyLineHeight
        };
      };
    },
    cssExportCode() {
      // Generate CSS variables for colors, typography, and spacing
      let css = `:root {\n`;
      
      // Colors
      css += `  /* Colors */\n`;
      for (const [key, value] of Object.entries(this.designSystem.colors)) {
        if (typeof value === 'string') { // Skip arrays like primaryShades
          css += `  --color-${key}: ${value};\n`;
        }
      }
      
      // Add color shades
      if (this.designSystem.colors.primaryShades?.length) {
        css += `\n  /* Primary Color Shades */\n`;
        this.designSystem.colors.primaryShades.forEach(shade => {
          css += `  --color-${shade.name}: ${shade.value};\n`;
        });
      }
      
      if (this.designSystem.colors.secondaryShades?.length) {
        css += `\n  /* Secondary Color Shades */\n`;
        this.designSystem.colors.secondaryShades.forEach(shade => {
          css += `  --color-${shade.name}: ${shade.value};\n`;
        });
      }
      
      if (this.designSystem.colors.neutralShades?.length) {
        css += `\n  /* Neutral Color Shades */\n`;
        this.designSystem.colors.neutralShades.forEach(shade => {
          css += `  --color-${shade.name}: ${shade.value};\n`;
        });
      }
      
      // Typography
      css += `\n  /* Typography */\n`;
      css += `  --font-heading: ${this.designSystem.typography.headingFont};\n`;
      css += `  --font-body: ${this.designSystem.typography.bodyFont};\n`;
      css += `  --font-ui: ${this.designSystem.typography.uiFont};\n`;
      css += `  --font-base-size: ${this.designSystem.typography.baseSize}px;\n`;
      css += `  --font-scale-ratio: ${this.designSystem.typography.scaleRatio};\n`;
      css += `  --heading-line-height: ${this.designSystem.typography.headingLineHeight};\n`;
      css += `  --body-line-height: ${this.designSystem.typography.bodyLineHeight};\n`;
      
      // Font sizes based on calculated scale
      css += `  --font-size-h1: ${this.calculatedSizes.h1}px;\n`;
      css += `  --font-size-h2: ${this.calculatedSizes.h2}px;\n`;
      css += `  --font-size-h3: ${this.calculatedSizes.h3}px;\n`;
      css += `  --font-size-h4: ${this.calculatedSizes.h4}px;\n`;
      css += `  --font-size-h5: ${this.calculatedSizes.h5}px;\n`;
      css += `  --font-size-h6: ${this.calculatedSizes.h6}px;\n`;
      css += `  --font-size-large: ${this.calculatedSizes.large}px;\n`;
      css += `  --font-size-small: ${this.calculatedSizes.small}px;\n`;
      
      // Spacing
      css += `\n  /* Spacing */\n`;
      css += `  --spacing-base-unit: ${this.designSystem.spacing.baseUnit}px;\n`;
      
      // Spacing values
      if (this.designSystem.spacing.values?.length) {
        this.designSystem.spacing.values.forEach((space, index) => {
          css += `  --spacing-${index + 1}: ${space.value}px;\n`;
        });
      }
      
      css += `}\n\n`;
      
      // Add common utility classes
      css += `/* Typography Utility Classes */\n`;
      css += `h1 { font-family: var(--font-heading); font-size: var(--font-size-h1); line-height: var(--heading-line-height); }\n`;
      css += `h2 { font-family: var(--font-heading); font-size: var(--font-size-h2); line-height: var(--heading-line-height); }\n`;
      css += `h3 { font-family: var(--font-heading); font-size: var(--font-size-h3); line-height: var(--heading-line-height); }\n`;
      css += `h4 { font-family: var(--font-heading); font-size: var(--font-size-h4); line-height: var(--heading-line-height); }\n`;
      css += `h5 { font-family: var(--font-heading); font-size: var(--font-size-h5); line-height: var(--heading-line-height); }\n`;
      css += `h6 { font-family: var(--font-heading); font-size: var(--font-size-h6); line-height: var(--heading-line-height); }\n`;
      css += `body { font-family: var(--font-body); font-size: var(--font-base-size); line-height: var(--body-line-height); }\n`;
      css += `.text-large { font-size: var(--font-size-large); }\n`;
      css += `.text-small { font-size: var(--font-size-small); }\n`;
      
      return css;
    },
    
    scssExportCode() {
      // Generate SCSS variables for colors, typography, and spacing
      let scss = `// Design System Variables\n\n`;
      
      // Colors
      scss += `// Colors\n`;
      for (const [key, value] of Object.entries(this.designSystem.colors)) {
        if (typeof value === 'string') { // Skip arrays like primaryShades
          scss += `$color-${key}: ${value};\n`;
        }
      }
      
      // Add color shades as maps
      scss += `\n// Color Shades\n`;
      scss += `$primary-shades: (\n`;
      if (this.designSystem.colors.primaryShades?.length) {
        this.designSystem.colors.primaryShades.forEach((shade, index) => {
          const comma = index < this.designSystem.colors.primaryShades.length - 1 ? ',' : '';
          scss += `  "${shade.name}": ${shade.value}${comma}\n`;
        });
      }
      scss += `);\n\n`;
      
      scss += `$secondary-shades: (\n`;
      if (this.designSystem.colors.secondaryShades?.length) {
        this.designSystem.colors.secondaryShades.forEach((shade, index) => {
          const comma = index < this.designSystem.colors.secondaryShades.length - 1 ? ',' : '';
          scss += `  "${shade.name}": ${shade.value}${comma}\n`;
        });
      }
      scss += `);\n\n`;
      
      scss += `$neutral-shades: (\n`;
      if (this.designSystem.colors.neutralShades?.length) {
        this.designSystem.colors.neutralShades.forEach((shade, index) => {
          const comma = index < this.designSystem.colors.neutralShades.length - 1 ? ',' : '';
          scss += `  "${shade.name}": ${shade.value}${comma}\n`;
        });
      }
      scss += `);\n\n`;
      
      // Typography
      scss += `// Typography\n`;
      scss += `$font-heading: ${this.designSystem.typography.headingFont};\n`;
      scss += `$font-body: ${this.designSystem.typography.bodyFont};\n`;
      scss += `$font-ui: ${this.designSystem.typography.uiFont};\n`;
      scss += `$font-base-size: ${this.designSystem.typography.baseSize}px;\n`;
      scss += `$font-scale-ratio: ${this.designSystem.typography.scaleRatio};\n`;
      scss += `$heading-line-height: ${this.designSystem.typography.headingLineHeight};\n`;
      scss += `$body-line-height: ${this.designSystem.typography.bodyLineHeight};\n\n`;
      
      // Font sizes map
      scss += `$font-sizes: (\n`;
      scss += `  "h1": ${this.calculatedSizes.h1}px,\n`;
      scss += `  "h2": ${this.calculatedSizes.h2}px,\n`;
      scss += `  "h3": ${this.calculatedSizes.h3}px,\n`;
      scss += `  "h4": ${this.calculatedSizes.h4}px,\n`;
      scss += `  "h5": ${this.calculatedSizes.h5}px,\n`;
      scss += `  "h6": ${this.calculatedSizes.h6}px,\n`;
      scss += `  "large": ${this.calculatedSizes.large}px,\n`;
      scss += `  "base": ${this.designSystem.typography.baseSize}px,\n`;
      scss += `  "small": ${this.calculatedSizes.small}px\n`;
      scss += `);\n\n`;
      
      // Spacing
      scss += `// Spacing\n`;
      scss += `$spacing-base-unit: ${this.designSystem.spacing.baseUnit}px;\n`;
      
      // Spacing map
      scss += `$spacing: (\n`;
      if (this.designSystem.spacing.values?.length) {
        this.designSystem.spacing.values.forEach((space, index) => {
          const comma = index < this.designSystem.spacing.values.length - 1 ? ',' : '';
          scss += `  ${index + 1}: ${space.value}px${comma}\n`;
        });
      }
      scss += `);\n\n`;
      
      // Add mixins and functions
      scss += `// Mixins and Functions\n`;
      scss += `@function spacing($level) {\n`;
      scss += `  @return map-get($spacing, $level);\n`;
      scss += `}\n\n`;
      
      scss += `@function color-shade($color, $shade) {\n`;
      scss += `  @if $color == "primary" {\n`;
      scss += `    @return map-get($primary-shades, $shade);\n`;
      scss += `  } @else if $color == "secondary" {\n`;
      scss += `    @return map-get($secondary-shades, $shade);\n`;
      scss += `  } @else if $color == "neutral" {\n`;
      scss += `    @return map-get($neutral-shades, $shade);\n`;
      scss += `  } @else {\n`;
      scss += `    @return null;\n`;
      scss += `  }\n`;
      scss += `}\n\n`;
      
      scss += `@mixin typography($size) {\n`;
      scss += `  font-size: map-get($font-sizes, $size);\n`;
      scss += `  @if $size == "h1" or $size == "h2" or $size == "h3" or $size == "h4" or $size == "h5" or $size == "h6" {\n`;
      scss += `    font-family: $font-heading;\n`;
      scss += `    line-height: $heading-line-height;\n`;
      scss += `  } @else {\n`;
      scss += `    font-family: $font-body;\n`;
      scss += `    line-height: $body-line-height;\n`;
      scss += `  }\n`;
      scss += `}\n`;
      
      return scss;
    }
  },
  methods: {
    saveDesignSystem() {
      // Save to localStorage
      localStorage.setItem('artsy-design-system', JSON.stringify(this.designSystem));
      this.isSaved = true;
      this.lastSaved = new Date();
      
      alert('Design system saved successfully!');
    },
    exportDesignSystem() {
      alert('Export functionality will be implemented in a later step');
    },
    generateShades(colorType) {
      // Generate 5 shades for the selected color (lighter to darker)
      const baseColor = this.designSystem.colors[colorType];
      const shades = [];
      
      // Convert hex to HSL for easier shade generation
      const hsl = this.hexToHSL(baseColor);
      
      // Generate 2 lighter shades and 3 darker shades
      const lightnessValues = [90, 70, 50, 30, 10]; // Values from light to dark
      
      for (let i = 0; i < 5; i++) {
        const lightness = lightnessValues[i];
        const shadeName = i < 2 
          ? `${colorType}-lighter-${i+1}` 
          : i === 2 
            ? `${colorType}-base` 
            : `${colorType}-darker-${i-2}`;
        
        const shadeValue = this.hslToHex(hsl.h, hsl.s, lightness);
        
        shades.push({
          name: shadeName,
          value: shadeValue
        });
      }
      
      this.designSystem.colors[`${colorType}Shades`] = shades;
    },
    hexToHSL(hex) {
      // Convert hex to RGB first
      let r = 0, g = 0, b = 0;
      if (hex.length === 4) {
        r = parseInt(hex[1] + hex[1], 16);
        g = parseInt(hex[2] + hex[2], 16);
        b = parseInt(hex[3] + hex[3], 16);
      } else if (hex.length === 7) {
        r = parseInt(hex.substring(1, 3), 16);
        g = parseInt(hex.substring(3, 5), 16);
        b = parseInt(hex.substring(5, 7), 16);
      }
      
      // Convert RGB to HSL
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
    hslToHex(h, s, l) {
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
      
      const toHex = x => {
        const hex = Math.round(x * 255).toString(16);
        return hex.length === 1 ? '0' + hex : hex;
      };
      
      return `#${toHex(r)}${toHex(g)}${toHex(b)}`;
    },
    updateTypographyPreview() {
      // Calculate font sizes based on the type scale ratio
      const { baseSize, scaleRatio } = this.designSystem.typography;
      
      // For headings (increasing sizes)
      this.calculatedSizes.h6 = Math.round(baseSize * Math.pow(scaleRatio, -1));
      this.calculatedSizes.h5 = Math.round(baseSize);
      this.calculatedSizes.h4 = Math.round(baseSize * Math.pow(scaleRatio, 1));
      this.calculatedSizes.h3 = Math.round(baseSize * Math.pow(scaleRatio, 2));
      this.calculatedSizes.h2 = Math.round(baseSize * Math.pow(scaleRatio, 3));
      this.calculatedSizes.h1 = Math.round(baseSize * Math.pow(scaleRatio, 4));
      
      // For body text
      this.calculatedSizes.large = Math.round(baseSize * 1.25);
      this.calculatedSizes.small = Math.round(baseSize * 0.875);
    },
    updateSpacingScale() {
      // Generate spacing values based on the scale type and base unit
      const { baseUnit, scaleType, scaleFactor, levels } = this.designSystem.spacing;
      const spacingValues = [];
      
      for (let i = 0; i < levels; i++) {
        let value;
        let name;
        
        if (scaleType === 'linear') {
          // Linear scale: baseUnit, baseUnit*2, baseUnit*3, etc.
          value = baseUnit * (i + 1);
          name = `space-${i + 1}`;
        } else {
          // Geometric scale: baseUnit, baseUnit*2, baseUnit*4, baseUnit*8, etc.
          value = Math.round(baseUnit * Math.pow(scaleFactor, i));
          name = `space-${i + 1}`;
        }
        
        spacingValues.push({
          name,
          value
        });
      }
      
      this.designSystem.spacing.values = spacingValues;
    },
    generateExportPreview() {
      switch (this.selectedExportFormat) {
        case 'css':
          return this.cssExportCode;
        case 'scss':
          return this.scssExportCode;
        case 'json':
          return JSON.stringify(this.designSystem, null, 2);
        default:
          return 'Select a format to see preview';
      }
    },
    copyExportCode() {
      const code = this.generateExportPreview();
      
      navigator.clipboard.writeText(code)
        .then(() => {
          alert('Export code copied to clipboard!');
        })
        .catch(err => {
          console.error('Failed to copy export code: ', err);
        });
    },
    downloadExportFile() {
      const format = this.exportFormats.find(f => f.id === this.selectedExportFormat);
      const data = this.generateExportPreview();
      let fileName = `design-system-export.${format.id}`;
      
      // Create a blob and download the file
      const blob = new Blob([data], { type: 'text/plain;charset=utf-8' });
      if (window.navigator && window.navigator.msSaveOrOpenBlob) {
        // For IE and Edge
        window.navigator.msSaveOrOpenBlob(blob, fileName);
      } else {
        // For other browsers
        const link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = fileName;
        link.click();
        URL.revokeObjectURL(link.href);
      }
    }
  },
  mounted() {
    // Load saved design system if available
    const savedSystem = localStorage.getItem('artsy-design-system');
    if (savedSystem) {
      try {
        this.designSystem = JSON.parse(savedSystem);
      } catch (e) {
        console.error('Failed to load saved design system', e);
      }
    }
    
    // Generate color shades for default colors if they don't exist
    if (!this.designSystem.colors.primaryShades || this.designSystem.colors.primaryShades.length === 0) {
      this.generateShades('primary');
    }
    if (!this.designSystem.colors.secondaryShades || this.designSystem.colors.secondaryShades.length === 0) {
      this.generateShades('secondary');
    }
    if (!this.designSystem.colors.neutralShades || this.designSystem.colors.neutralShades.length === 0) {
      this.generateShades('neutral');
    }
    
    // Initialize calculated sizes for typography preview
    this.calculatedSizes = {
      h1: 32,
      h2: 24,
      h3: 18.72,
      h4: 16,
      h5: 13.28,
      h6: 10.72,
      large: 18.72,
      small: 13.28
    };
    
    this.updateTypographyPreview();
    this.updateSpacingScale();
  }
}
</script>

<style scoped>
.design-system-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
  color: #333;
}

h1 {
  text-align: center;
  margin-bottom: 10px;
}

h2 {
  margin-top: 0;
  margin-bottom: 15px;
  color: #444;
}

.instructions {
  text-align: center;
  color: #666;
  margin-bottom: 30px;
}

.section-desc {
  color: #666;
  margin-bottom: 25px;
  max-width: 700px;
}

.design-system-grid {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 30px;
  background-color: #f5f5f5;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Sidebar styles */
.sidebar {
  background-color: #333;
  color: white;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 600px;
}

.section-nav {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.section-nav button {
  background-color: transparent;
  color: white;
  border: none;
  padding: 12px 15px;
  text-align: left;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.section-nav button:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.section-nav button.active {
  background-color: #e91e63;
  font-weight: bold;
}

.action-buttons {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 20px;
}

.save-btn, .export-btn {
  padding: 12px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s;
}

.save-btn {
  background-color: #4CAF50;
  color: white;
}

.save-btn:hover {
  background-color: #45a049;
}

.export-btn {
  background-color: #2196F3;
  color: white;
}

.export-btn:hover {
  background-color: #0b7dda;
}

/* Content area styles */
.content-area {
  background-color: white;
  padding: 30px;
  border-radius: 0 8px 8px 0;
}

.section {
  margin-bottom: 40px;
}

.placeholder-content {
  background-color: #f9f9f9;
  border: 2px dashed #ddd;
  border-radius: 8px;
  padding: 40px;
  text-align: center;
  color: #999;
  font-style: italic;
}

/* Color section styles */
.color-groups {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.color-group {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.color-group h3 {
  margin-top: 0;
  margin-bottom: 10px;
  color: #333;
}

.group-desc {
  color: #666;
  margin-top: 0;
  margin-bottom: 20px;
  font-size: 14px;
}

.color-row {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  align-items: center;
}

.color-item {
  position: relative;
  background-color: white;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.2s;
}

.color-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.main-color {
  width: 140px;
  height: 140px;
}

.shade {
  width: 110px;
  height: 110px;
}

.semantic-color {
  width: 120px;
  height: 120px;
}

.color-preview {
  height: 65%;
  width: 100%;
  cursor: pointer;
}

.color-info {
  padding: 8px;
  background-color: white;
  height: 35%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.color-label {
  font-size: 12px;
  color: #666;
  margin-bottom: 2px;
}

.color-value {
  font-family: monospace;
  font-size: 12px;
  color: #333;
}

.color-picker {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
}

.semantic-colors {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

/* Typography section styles */
.typography-settings {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.settings-group {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.settings-group h3 {
  margin-top: 0;
  margin-bottom: 10px;
  color: #333;
}

.settings-desc {
  color: #666;
  margin-top: 0;
  margin-bottom: 20px;
  font-size: 14px;
}

.font-families {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.font-family-item {
  display: flex;
  flex-direction: column;
  background-color: white;
  border-radius: 4px;
  padding: 15px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.font-family-item label {
  font-size: 14px;
  color: #333;
  margin-bottom: 5px;
}

.font-family-item select {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
}

.font-preview {
  margin-top: 10px;
  font-size: 18px;
  color: #333;
}

.size-selector, .scale-selector {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.size-selector label, .scale-selector label {
  font-size: 14px;
  color: #333;
}

.size-selector input, .scale-selector select {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
}

.size-range {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  color: #666;
}

.line-height-settings {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.line-height-item {
  display: flex;
  flex-direction: column;
}

.line-height-item label {
  font-size: 14px;
  color: #333;
  margin-bottom: 5px;
}

.line-height-item input {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
}

.typography-preview {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
  margin-top: 30px;
}

.typography-preview h1, 
.typography-preview h2, 
.typography-preview h3, 
.typography-preview h4, 
.typography-preview h5, 
.typography-preview h6 {
  margin-top: 0;
}

.preview-title {
  margin-top: 0;
  margin-bottom: 15px;
  color: #333;
}

.type-preview-content {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.text-sample {
  padding: 10px;
  background-color: white;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Spacing section styles */
.spacing-settings {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.base-unit-control, .scale-type-control, .factor-control, .levels-control {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.scale-option {
  display: flex;
  align-items: center;
  gap: 10px;
}

.spacing-preview {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.spacing-scale {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.spacing-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.spacing-visual {
  flex-grow: 1;
  height: 8px;
  background-color: #ddd;
  border-radius: 4px;
}

.spacing-bar {
  height: 100%;
  background-color: #2196F3;
  border-radius: 4px;
}

.spacing-info {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.spacing-name {
  font-size: 14px;
  color: #333;
}

.spacing-value {
  font-family: monospace;
  font-size: 14px;
  color: #333;
}

.examples-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}

.example-card {
  background-color: #fff;
  border-radius: 8px;
  padding: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.example-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  border: 2px dashed #ddd;
  border-radius: 4px;
  margin-bottom: 10px;
}

.example-box {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  border-radius: 4px;
  transition: transform 0.2s;
}

.example-box:hover {
  transform: scale(1.05);
}

.example-code {
  font-family: monospace;
  font-size: 14px;
  color: #333;
  background-color: #f4f4f4;
  padding: 10px;
  border-radius: 4px;
  overflow-x: auto;
}

/* Components section styles */
.components-preview {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.component-row {
  display: flex;
  flex-wrap: wrap;
  gap: 30px;
}

.component-group {
  flex: 1;
  min-width: 250px;
}

.component-samples {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.ds-button {
  font-family: inherit;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s, transform 0.2s;
}

.ds-button:hover {
  transform: translateY(-2px);
}

.ds-primary {
  background-color: #3f51b5;
  color: white;
}

.ds-secondary {
  background-color: #ff4081;
  color: white;
}

.ds-outlined {
  background-color: transparent;
  color: #3f51b5;
  border: 2px solid #3f51b5;
}

.ds-text {
  background-color: transparent;
  color: #3f51b5;
}

/* Card styles */
.ds-card {
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.ds-card-header {
  padding: 15px;
  background-color: #f5f5f5;
  border-bottom: 1px solid #ddd;
}

.ds-card-content {
  padding: 15px;
  font-size: 14px;
  color: #333;
}

.ds-card-actions {
  padding: 10px 15px;
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}

/* Form control styles */
.ds-form-group {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.ds-checkbox {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* Alert styles */
.ds-alert {
  padding: 15px;
  border-radius: 4px;
  font-size: 14px;
  margin-bottom: 10px;
}

/* Navigation styles */
.ds-nav {
  display: flex;
  align-items: center;
  padding: 10px 15px;
  background-color: #3f51b5;
  color: white;
}

.ds-nav-brand {
  font-weight: bold;
  font-size: 18px;
  margin-right: 20px;
}

.ds-nav-links {
  display: flex;
  gap: 15px;
}

.ds-nav-link {
  color: white;
  text-decoration: none;
  transition: color 0.2s;
}

.ds-nav-link:hover {
  color: #ff4081;
}

/* Export section styles */
.export-options {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.format-selector {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

.format-option {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 15px;
  flex: 1;
  min-width: 150px;
  cursor: pointer;
  transition: transform 0.2s;
}

.format-option:hover {
  transform: translateY(-2px);
}

.format-option.active {
  background-color: #e3f2fd;
  border: 2px solid #2196F3;
}

.format-icon {
  font-size: 24px;
  margin-bottom: 10px;
}

.export-preview {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.code-preview {
  font-family: monospace;
  font-size: 14px;
  color: #333;
  background-color: #f4f4f4;
  padding: 10px;
  border-radius: 4px;
  overflow-x: auto;
}

.export-actions {
  display: flex;
  gap: 10px;
}

.copy-btn, .download-btn {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s;
}

.copy-btn {
  background-color: #4CAF50;
  color: white;
}

.copy-btn:hover {
  background-color: #45a049;
}

.download-btn {
  background-color: #2196F3;
  color: white;
}

.download-btn:hover {
  background-color: #0b7dda;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .design-system-grid {
    grid-template-columns: 1fr;
  }
  
  .sidebar {
    min-height: auto;
    border-radius: 8px 8px 0 0;
  }
  
  .content-area {
    border-radius: 0 0 8px 8px;
  }
}
</style>