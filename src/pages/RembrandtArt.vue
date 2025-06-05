<template>
  <div class="rembrandt-container">
    <h1>Dutch Masters in CSS</h1>
    
    <!-- Rembrandt's Night Watch -->
    <div class="art-piece night-watch">
      <div class="frame">
        <div class="canvas">
          <!-- Main group of figures -->
          <div class="central-figures">
            <!-- Captain Frans Banning Cocq -->
            <div class="captain">
              <div class="captain-hat"></div>
              <div class="captain-face"></div>
              <div class="captain-body"></div>
              <div class="captain-arm"></div>
              <div class="captain-legs"></div>
              <div class="captain-hand"></div>
            </div>
            
            <!-- Lieutenant Willem van Ruytenburch -->
            <div class="lieutenant">
              <div class="lieutenant-hat"></div>
              <div class="lieutenant-face"></div>
              <div class="lieutenant-body"></div>
              <div class="lieutenant-legs"></div>
            </div>
            
            <!-- Little girl (the hidden figure) -->
            <div class="girl"></div>
            
            <!-- The drummer -->
            <div class="drummer">
              <div class="drummer-body"></div>
              <div class="drummer-head"></div>
              <div class="drum"></div>
            </div>
            
            <!-- Musket bearers -->
            <div class="musketeer m1">
              <div class="musket"></div>
            </div>
            <div class="musketeer m2">
              <div class="musket"></div>
            </div>
            <div class="musketeer m3">
              <div class="musket"></div>
            </div>
            
            <!-- Flag bearer -->
            <div class="flag-bearer">
              <div class="flag"></div>
            </div>
          </div>
          
          <!-- Background elements -->
          <div class="background">
            <div class="archway"></div>
            <div class="shadow-left"></div>
            <div class="shadow-right"></div>
            <div class="light-beam"></div>
          </div>
          
          <!-- Foreground details -->
          <div class="foreground">
            <div class="dog"></div>
            <div class="shadow-floor"></div>
          </div>
        </div>
      </div>
      <p class="art-title">Rembrandt van Rijn's "The Night Watch" (1642)</p>
      <p class="art-description">
        This CSS recreation captures the dramatic chiaroscuro lighting, complex composition, and dynamic movement of Rembrandt's most famous painting. Originally titled "Militia Company of District II under the Command of Captain Frans Banninck Cocq," the painting depicts the civic guard moving out, with the dramatic use of light and shadow enhancing its theatrical quality.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RembrandtArt'
}
</script>

<style scoped>
.rembrandt-container {
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
  width: 700px;
  height: 520px; /* Adjusted for the painting's proportions */
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(45deg, #3d2c14, #654321, #3d2c14);
  box-shadow: 
    0 0 0 1px #2a1a0a,
    inset 0 0 15px rgba(0, 0, 0, 0.4),
    5px 5px 15px rgba(0, 0, 0, 0.3);
  border-radius: 3px;
}

.canvas {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background-color: #170f0b;
  box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.6);
}

/* Night Watch specific elements */
.night-watch .background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.archway {
  position: absolute;
  top: 5%;
  left: 25%;
  width: 50%;
  height: 60%;
  background: linear-gradient(to bottom, 
    #372213 0%, 
    #241509 100%);
  border-radius: 50% 50% 0 0 / 60% 60% 0 0;
  opacity: 0.7;
}

.shadow-left {
  position: absolute;
  top: 0;
  left: 0;
  width: 25%;
  height: 100%;
  background: linear-gradient(to right, 
    rgba(15, 8, 3, 0.9) 0%, 
    rgba(15, 8, 3, 0) 100%);
}

.shadow-right {
  position: absolute;
  top: 0;
  right: 0;
  width: 30%;
  height: 100%;
  background: linear-gradient(to left, 
    rgba(15, 8, 3, 0.8) 0%, 
    rgba(15, 8, 3, 0) 100%);
}

.light-beam {
  position: absolute;
  top: 10%;
  left: 35%;
  width: 30%;
  height: 100%;
  background: radial-gradient(
    ellipse at top,
    rgba(255, 230, 180, 0.15) 0%,
    rgba(255, 230, 180, 0.05) 50%,
    rgba(255, 230, 180, 0) 70%
  );
  transform: rotate(-10deg);
}

/* Central figures */
.central-figures {
  position: absolute;
  bottom: 5%;
  left: 0;
  width: 100%;
  height: 90%;
}

/* Captain Frans Banning Cocq */
.captain {
  position: absolute;
  bottom: 5%;
  left: 30%;
  width: 12%;
  height: 60%;
}

.captain-hat {
  position: absolute;
  top: 0;
  left: 15%;
  width: 70%;
  height: 10%;
  background-color: #1c1006;
  border-radius: 50% 50% 0 0;
}

.captain-face {
  position: absolute;
  top: 10%;
  left: 25%;
  width: 50%;
  height: 15%;
  background-color: #d8bda0;
  border-radius: 40% 40% 30% 30%;
}

.captain-body {
  position: absolute;
  top: 25%;
  left: 20%;
  width: 60%;
  height: 40%;
  background-color: #111;
  border-radius: 10% 10% 0 0;
}

.captain-arm {
  position: absolute;
  top: 30%;
  left: 80%;
  width: 50%;
  height: 10%;
  background-color: #111;
  transform: rotate(20deg);
}

.captain-hand {
  position: absolute;
  top: 28%;
  left: 125%;
  width: 15%;
  height: 7%;
  background-color: #d8bda0;
  border-radius: 50%;
}

.captain-legs {
  position: absolute;
  top: 65%;
  left: 20%;
  width: 60%;
  height: 35%;
  background-color: #1a1105;
}

/* Lieutenant Willem van Ruytenburch */
.lieutenant {
  position: absolute;
  bottom: 5%;
  left: 42%;
  width: 12%;
  height: 58%;
}

.lieutenant-hat {
  position: absolute;
  top: 2%;
  left: 15%;
  width: 70%;
  height: 8%;
  background-color: #d8bc84;
  border-radius: 50% 50% 0 0;
}

.lieutenant-face {
  position: absolute;
  top: 11%;
  left: 25%;
  width: 50%;
  height: 14%;
  background-color: #d8bda0;
  border-radius: 40% 40% 30% 30%;
}

.lieutenant-body {
  position: absolute;
  top: 25%;
  left: 15%;
  width: 70%;
  height: 40%;
  background-color: #e9d197;
  border-radius: 10% 10% 0 0;
}

.lieutenant-legs {
  position: absolute;
  top: 65%;
  left: 15%;
  width: 70%;
  height: 35%;
  background-color: #e9d197;
}

/* The drummer */
.drummer {
  position: absolute;
  bottom: 10%;
  right: 20%;
  width: 10%;
  height: 40%;
}

.drummer-body {
  position: absolute;
  top: 20%;
  left: 0;
  width: 100%;
  height: 60%;
  background-color: #633d28;
}

.drummer-head {
  position: absolute;
  top: 5%;
  left: 25%;
  width: 50%;
  height: 15%;
  background-color: #d8bda0;
  border-radius: 50%;
}

.drum {
  position: absolute;
  top: 60%;
  left: -50%;
  width: 120%;
  height: 25%;
  background: linear-gradient(to bottom, 
    #9b7b4e 0%, 
    #7d5e2f 50%, 
    #9b7b4e 100%);
  border-radius: 5px;
}

/* Musket bearers */
.musketeer {
  position: absolute;
  bottom: 10%;
  width: 8%;
  height: 45%;
}

.m1 {
  left: 15%;
}

.m2 {
  left: 55%;
}

.m3 {
  right: 10%;
}

.musketeer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 25%;
  width: 50%;
  height: 15%;
  background-color: #d8bda0;
  border-radius: 50%;
}

.musketeer::after {
  content: '';
  position: absolute;
  top: 15%;
  left: 0;
  width: 100%;
  height: 85%;
  background-color: #3d2e1a;
}

.musket {
  position: absolute;
  top: -20%;
  left: 45%;
  width: 5%;
  height: 80%;
  background-color: #2a1d10;
  transform-origin: bottom;
  transform: rotate(-5deg);
}

/* Flag bearer */
.flag-bearer {
  position: absolute;
  bottom: 10%;
  left: 63%;
  width: 8%;
  height: 50%;
}

.flag-bearer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 25%;
  width: 50%;
  height: 15%;
  background-color: #d8bda0;
  border-radius: 50%;
}

.flag-bearer::after {
  content: '';
  position: absolute;
  top: 15%;
  left: 0;
  width: 100%;
  height: 85%;
  background-color: #5a3520;
}

.flag {
  position: absolute;
  top: -30%;
  left: -100%;
  width: 150%;
  height: 50%;
  background: linear-gradient(135deg, 
    #a03e1f 0%, 
    #b8522d 50%, 
    #c8622d 100%);
  clip-path: polygon(0 0, 100% 0, 80% 100%, 0 100%);
  transform-origin: bottom right;
  transform: rotate(-5deg);
}

/* Little girl (the hidden figure) */
.girl {
  position: absolute;
  bottom: 20%;
  left: 47%;
  width: 5%;
  height: 25%;
  background-color: #e9d197;
  opacity: 0.6;
  border-radius: 30% 30% 0 0;
  z-index: 10;
}

.girl::before {
  content: '';
  position: absolute;
  top: 0;
  left: 25%;
  width: 50%;
  height: 30%;
  background-color: #d8bda0;
  border-radius: 50%;
}

/* Dog */
.dog {
  position: absolute;
  bottom: 2%;
  left: 10%;
  width: 6%;
  height: 8%;
  background-color: #402818;
  border-radius: 30% 30% 0 50%;
  transform: scaleX(1.5);
}

.dog::before {
  content: '';
  position: absolute;
  top: -30%;
  left: 60%;
  width: 40%;
  height: 30%;
  background-color: #402818;
  border-radius: 50%;
}

.dog::after {
  content: '';
  position: absolute;
  top: 0;
  right: -30%;
  width: 40%;
  height: 70%;
  background-color: #402818;
  border-radius: 0 30% 30% 0;
}

/* Shadow on floor */
.shadow-floor {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 8%;
  background: linear-gradient(to bottom, 
    rgba(0, 0, 0, 0) 0%, 
    rgba(0, 0, 0, 0.8) 100%);
}

/* Media query for responsiveness */
@media (max-width: 750px) {
  .frame {
    width: 500px;
    height: 380px;
  }
}

@media (max-width: 550px) {
  .frame {
    width: 320px;
    height: 240px;
  }
}
</style>