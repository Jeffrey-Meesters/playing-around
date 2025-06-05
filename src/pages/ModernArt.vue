<template>
  <div class="modern-art-container">
    <h1>Modern Abstract CSS Art</h1>
    
    <!-- Neo-Mondrian -->
    <div class="art-piece neo-mondrian">
      <div class="frame">
        <div class="canvas">
          <!-- Grid structure -->
          <div class="grid-container">
            <!-- Row 1 -->
            <div class="grid-cell r1c1"></div>
            <div class="grid-cell r1c2"></div>
            <div class="grid-cell r1c3"></div>
            <div class="grid-cell r1c4"></div>
            <div class="grid-cell r1c5"></div>
            
            <!-- Row 2 -->
            <div class="grid-cell r2c1"></div>
            <div class="grid-cell r2c2"></div>
            <div class="grid-cell r2c3"></div>
            <div class="grid-cell r2c4"></div>
            <div class="grid-cell r2c5"></div>
            
            <!-- Row 3 -->
            <div class="grid-cell r3c1"></div>
            <div class="grid-cell r3c2"></div>
            <div class="grid-cell r3c3"></div>
            <div class="grid-cell r3c4"></div>
            <div class="grid-cell r3c5"></div>
            
            <!-- Row 4 -->
            <div class="grid-cell r4c1"></div>
            <div class="grid-cell r4c2"></div>
            <div class="grid-cell r4c3"></div>
            <div class="grid-cell r4c4"></div>
            <div class="grid-cell r4c5"></div>
            
            <!-- Row 5 -->
            <div class="grid-cell r5c1"></div>
            <div class="grid-cell r5c2"></div>
            <div class="grid-cell r5c3"></div>
            <div class="grid-cell r5c4"></div>
            <div class="grid-cell r5c5"></div>
            
            <!-- Grid lines -->
            <div class="grid-line vertical v1"></div>
            <div class="grid-line vertical v2"></div>
            <div class="grid-line vertical v3"></div>
            <div class="grid-line vertical v4"></div>
            <div class="grid-line horizontal h1"></div>
            <div class="grid-line horizontal h2"></div>
            <div class="grid-line horizontal h3"></div>
            <div class="grid-line horizontal h4"></div>
            
            <!-- Floating elements -->
            <div class="floating-element circle c1"></div>
            <div class="floating-element circle c2"></div>
            <div class="floating-element circle c3"></div>
          </div>
        </div>
      </div>
      <p class="art-title">Neo-Mondrian Composition with Digital Elements</p>
      <p class="art-description">
        This piece reimagines Piet Mondrian's geometric abstraction style with a modern digital twist. 
        The traditional primary color blocks and black grid lines are enhanced with floating circular elements 
        and subtle gradients that break the rigid structure, representing how digital technology 
        disrupts established frameworks.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModernArt'
}
</script>

<style scoped>
.modern-art-container {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

h1 {
  text-align: center;
  margin-bottom: 40px;
  color: #333;
}

.art-piece {
  margin-bottom: 60px;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.art-title {
  text-align: center;
  font-size: 1.4rem;
  margin-top: 30px;
  margin-bottom: 5px;
  font-weight: bold;
  color: #444;
}

.art-description {
  text-align: center;
  font-size: 1rem;
  line-height: 1.5;
  color: #666;
  max-width: 800px;
  margin: 0 auto;
}

/* Frame and canvas */
.frame {
  width: 600px;
  height: 600px;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(45deg, #e0e0e0, #f8f8f8, #e0e0e0);
  box-shadow: 
    0 0 0 1px #999,
    inset 0 0 10px rgba(0, 0, 0, 0.2),
    5px 5px 20px rgba(0, 0, 0, 0.2);
  border-radius: 3px;
}

.canvas {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background-color: #ffffff;
  box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.1);
}

/* Neo-Mondrian grid */
.grid-container {
  position: relative;
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: 1.5fr 1fr 2fr 1fr 1.5fr;
  grid-template-rows: 1fr 1.5fr 1.2fr 1.8fr 1fr;
  gap: 0;
}

.grid-cell {
  position: relative;
  background-color: white;
  transition: background-color 0.5s ease;
}

/* Colored cells */
.r1c1 {
  background-color: #ffeb3b; /* Yellow */
}

.r1c5 {
  background: linear-gradient(135deg, #2196f3, #03a9f4); /* Blue gradient */
}

.r2c2 {
  background-color: #f44336; /* Red */
}

.r3c3 {
  background: linear-gradient(45deg, #f44336, #ff9800); /* Red-orange gradient */
}

.r3c4, .r3c5, .r4c5 {
  background-color: #ffffff; /* White */
}

.r4c1 {
  background: linear-gradient(90deg, #2196f3, #4caf50); /* Blue-green gradient */
}

.r5c2 {
  background-color: #4caf50; /* Green */
}

.r5c5 {
  background-color: #2196f3; /* Blue */
}

/* Grid lines */
.grid-line {
  position: absolute;
  background-color: #111;
  z-index: 2;
}

.vertical {
  width: 8px;
  height: 100%;
  top: 0;
}

.horizontal {
  width: 100%;
  height: 8px;
  left: 0;
}

.v1 {
  left: 20%;
}

.v2 {
  left: 40%;
}

.v3 {
  left: 60%;
}

.v4 {
  left: 80%;
}

.h1 {
  top: 20%;
}

.h2 {
  top: 40%;
}

.h3 {
  top: 60%;
}

.h4 {
  top: 80%;
}

/* Floating elements */
.floating-element {
  position: absolute;
  z-index: 3;
  filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.3));
}

.circle {
  border-radius: 50%;
}

.c1 {
  width: 80px;
  height: 80px;
  top: 15%;
  left: 25%;
  background: radial-gradient(circle at 30% 30%, #ff9800, #f44336);
  animation: float1 8s ease-in-out infinite;
}

.c2 {
  width: 60px;
  height: 60px;
  top: 45%;
  left: 65%;
  background: radial-gradient(circle at 30% 30%, #4caf50, #2196f3);
  animation: float2 10s ease-in-out infinite;
}

.c3 {
  width: 40px;
  height: 40px;
  top: 70%;
  left: 35%;
  background: radial-gradient(circle at 30% 30%, #ffeb3b, #ff9800);
  animation: float3 7s ease-in-out infinite;
}

@keyframes float1 {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(20px, 15px); }
}

@keyframes float2 {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(-15px, 20px); }
}

@keyframes float3 {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(10px, -15px); }
}

/* Media query for responsiveness */
@media (max-width: 700px) {
  .frame {
    width: 450px;
    height: 450px;
  }

  .c1 {
    width: 60px;
    height: 60px;
  }

  .c2 {
    width: 45px;
    height: 45px;
  }

  .c3 {
    width: 30px;
    height: 30px;
  }
}

@media (max-width: 500px) {
  .frame {
    width: 320px;
    height: 320px;
  }

  .grid-line.vertical {
    width: 5px;
  }

  .grid-line.horizontal {
    height: 5px;
  }

  .c1 {
    width: 40px;
    height: 40px;
  }

  .c2 {
    width: 30px;
    height: 30px;
  }

  .c3 {
    width: 20px;
    height: 20px;
  }
}
</style>