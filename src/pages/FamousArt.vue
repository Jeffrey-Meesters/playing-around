<template>
  <div class="famous-art-container">
    <h1>Famous Art Masterpieces in CSS</h1>
    
    <!-- Van Gogh's Starry Night -->
    <div class="art-piece starry-night">
      <div class="frame">
        <div class="canvas">
          <div class="sky">
            <div class="stars s1"></div>
            <div class="stars s2"></div>
            <div class="stars s3"></div>
            <div class="stars s4"></div>
            <div class="stars s5"></div>
            <div class="moon"></div>
            <div class="swirl sw1"></div>
            <div class="swirl sw2"></div>
            <div class="swirl sw3"></div>
            <div class="swirl sw4"></div>
          </div>
          <div class="village">
            <div class="buildings">
              <div class="house h1"></div>
              <div class="house h2"></div>
              <div class="house h3"></div>
              <div class="house h4"></div>
              <div class="house h5"></div>
            </div>
            <div class="church">
              <div class="church-base"></div>
              <div class="steeple"></div>
            </div>
          </div>
          <div class="hills">
            <div class="hill h1"></div>
            <div class="hill h2"></div>
          </div>
          <div class="cypress">
            <div class="cypress-trunk"></div>
            <div class="cypress-top"></div>
          </div>
        </div>
      </div>
      <p class="art-title">Vincent van Gogh's "Starry Night" (1889)</p>
      <p class="art-description">
        This CSS interpretation of Vincent van Gogh's masterpiece captures the swirling night sky, 
        the quiet village below, and the iconic cypress tree that together create one of the most 
        recognizable paintings in Western culture.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FamousArt'
}
</script>

<style scoped>
.famous-art-container {
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

.frame {
  width: 600px;
  height: 450px;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(45deg, #8b6b3d, #c7a55e, #8b6b3d);
  box-shadow: 
    0 0 0 1px #5a4424,
    inset 0 0 15px rgba(0, 0, 0, 0.4),
    5px 5px 15px rgba(0, 0, 0, 0.3);
  border-radius: 3px;
}

.canvas {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background-color: #0f172a;
  box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.5);
}

/* Starry Night */
.starry-night .sky {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 65%;
  background: linear-gradient(to bottom, 
    #0b1631 0%, 
    #10244e 25%, 
    #1e3a7b 45%, 
    #2a4997 60%, 
    #355cb0 75%);
  overflow: hidden;
}

.stars {
  position: absolute;
  border-radius: 50%;
  background-color: #fff;
  box-shadow: 0 0 8px 2px rgba(255, 255, 240, 0.6);
}

.s1 {
  width: 8px;
  height: 8px;
  top: 15%;
  left: 25%;
  background-color: #ffffc0;
}

.s2 {
  width: 6px;
  height: 6px;
  top: 10%;
  left: 40%;
  background-color: #fff8e0;
}

.s3 {
  width: 10px;
  height: 10px;
  top: 25%;
  left: 60%;
  background-color: #ffffd0;
  box-shadow: 0 0 12px 4px rgba(255, 255, 210, 0.8);
}

.s4 {
  width: 7px;
  height: 7px;
  top: 35%;
  left: 75%;
  background-color: #fff9c0;
}

.s5 {
  width: 5px;
  height: 5px;
  top: 20%;
  left: 85%;
  background-color: #ffffd6;
}

.moon {
  position: absolute;
  top: 15%;
  right: 20%;
  width: 50px;
  height: 50px;
  background: radial-gradient(circle at center, 
    #ffffc0 0%, 
    #fff88e 40%, 
    #ffda4f 70%, 
    #ffb600 100%);
  border-radius: 50%;
  box-shadow: 0 0 30px 10px rgba(255, 200, 100, 0.6);
}

.swirl {
  position: absolute;
  border-radius: 50%;
  border: 10px solid transparent;
  border-top-color: #35509a;
  border-right-color: #3a5dac;
  opacity: 0.7;
  filter: blur(2px);
}

.sw1 {
  width: 160px;
  height: 160px;
  top: -40px;
  left: 30px;
  transform: rotate(30deg);
  border-width: 15px;
}

.sw2 {
  width: 140px;
  height: 140px;
  top: -20px;
  left: 200px;
  transform: rotate(-20deg);
  border-width: 12px;
}

.sw3 {
  width: 120px;
  height: 120px;
  top: 10px;
  right: 80px;
  transform: rotate(45deg);
  border-width: 18px;
}

.sw4 {
  width: 180px;
  height: 180px;
  top: 40px;
  left: 120px;
  transform: rotate(-45deg);
  border-width: 14px;
}

.swirl::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 80%;
  height: 80%;
  border-radius: 50%;
  background: radial-gradient(circle at center, 
    rgba(53, 92, 176, 0.1) 0%, 
    rgba(49, 85, 165, 0.3) 50%, 
    rgba(45, 78, 154, 0.1) 100%);
  transform: translate(-50%, -50%);
}

.village {
  position: absolute;
  bottom: 25%;
  left: 0;
  width: 100%;
  height: 15%;
}

.buildings {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.house {
  position: absolute;
  bottom: 0;
  background-color: #1c2e4a;
  border-radius: 2px 2px 0 0;
}

.h1 {
  height: 40px;
  width: 35px;
  left: 120px;
  background-color: #1e2e45;
}

.h2 {
  height: 50px;
  width: 40px;
  left: 160px;
  background-color: #1a2b40;
}

.h3 {
  height: 35px;
  width: 45px;
  left: 205px;
  background-color: #162538;
}

.h4 {
  height: 45px;
  width: 50px;
  left: 255px;
  background-color: #1a2a3c;
}

.h5 {
  height: 30px;
  width: 35px;
  left: 310px;
  background-color: #162335;
}

.house::before {
  content: '';
  position: absolute;
  top: 25%;
  left: 20%;
  width: 20%;
  height: 20%;
  background-color: rgba(255, 235, 132, 0.4);
  box-shadow: 0 0 5px rgba(255, 235, 132, 0.4);
}

.house::after {
  content: '';
  position: absolute;
  top: 25%;
  right: 20%;
  width: 20%;
  height: 20%;
  background-color: rgba(255, 235, 132, 0.4);
  box-shadow: 0 0 5px rgba(255, 235, 132, 0.4);
}

.church {
  position: absolute;
  bottom: 0;
  left: 380px;
  width: 40px;
  height: 120px;
  z-index: 10;
}

.church-base {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 80%;
  background-color: #102033;
  border-radius: 2px 2px 0 0;
}

.steeple {
  position: absolute;
  bottom: 80%;
  left: 30%;
  width: 40%;
  height: 80%;
  background-color: #0a1729;
  border-radius: 2px 2px 0 0;
}

.steeple::before {
  content: '';
  position: absolute;
  top: -15px;
  left: 50%;
  width: 3px;
  height: 15px;
  background-color: #071322;
  transform: translateX(-50%);
}

.hills {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 25%;
  overflow: hidden;
}

.hill {
  position: absolute;
  bottom: 0;
  border-radius: 50% 50% 0 0;
}

.h1 {
  width: 600px;
  height: 200px;
  left: -150px;
  background: linear-gradient(to bottom, #1a3045 0%, #25435c 100%);
  z-index: 1;
}

.h2 {
  width: 500px;
  height: 150px;
  right: -100px;
  background: linear-gradient(to bottom, #17293d 0%, #214054 100%);
  z-index: 2;
}

.cypress {
  position: absolute;
  bottom: 0;
  left: 40px;
  width: 60px;
  height: 250px;
  z-index: 5;
}

.cypress-trunk {
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 15px;
  height: 50px;
  background-color: #0d1d2c;
  transform: translateX(-50%);
}

.cypress-top {
  position: absolute;
  bottom: 40px;
  left: 0;
  width: 100%;
  height: 210px;
  background-color: #0f2030;
  clip-path: ellipse(25px 105px at center);
}

.cypress-top::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: 
    radial-gradient(
      ellipse at center, 
      rgba(20, 48, 75, 0.9) 0%,
      rgba(15, 32, 48, 0) 70%
    );
}

/* Media query for responsiveness */
@media (max-width: 700px) {
  .frame {
    width: 450px;
    height: 340px;
  }

  .swirl {
    transform-origin: center;
    transform: scale(0.8) rotate(30deg);
  }
  
  .sw2 {
    transform: scale(0.8) rotate(-20deg);
  }
  
  .sw3 {
    transform: scale(0.8) rotate(45deg);
  }
  
  .sw4 {
    transform: scale(0.8) rotate(-45deg);
  }
}

@media (max-width: 500px) {
  .frame {
    width: 320px;
    height: 240px;
  }
  
  .swirl {
    transform-origin: center;
    transform: scale(0.6) rotate(30deg);
  }
  
  .sw2 {
    transform: scale(0.6) rotate(-20deg);
  }
  
  .sw3 {
    transform: scale(0.6) rotate(45deg);
  }
  
  .sw4 {
    transform: scale(0.6) rotate(-45deg);
  }
}
</style>