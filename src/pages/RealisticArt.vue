<template>
  <div class="realistic-art-container">
    <h1>Realistic CSS Art Gallery</h1>
    
    <!-- City Skyline -->
    <div class="art-piece skyline">
      <div class="scene-container">
        <div class="sky">
          <div class="stars"></div>
          <div class="moon"></div>
        </div>
        <div class="buildings">
          <div class="building b1">
            <div class="windows"></div>
          </div>
          <div class="building b2">
            <div class="windows"></div>
          </div>
          <div class="building b3">
            <div class="antenna"></div>
            <div class="windows"></div>
          </div>
          <div class="building b4">
            <div class="windows"></div>
          </div>
          <div class="building b5">
            <div class="windows"></div>
          </div>
          <div class="building b6">
            <div class="windows"></div>
          </div>
        </div>
        <div class="ground"></div>
      </div>
      <p class="art-title">Night City Skyline</p>
    </div>
    
    <!-- Sunset Beach -->
    <div class="art-piece sunset-beach">
      <div class="scene-container">
        <div class="sunset-sky"></div>
        <div class="sun"></div>
        <div class="ocean">
          <div class="wave w1"></div>
          <div class="wave w2"></div>
          <div class="wave w3"></div>
        </div>
        <div class="beach"></div>
        <div class="palm-tree">
          <div class="trunk"></div>
          <div class="leaves l1"></div>
          <div class="leaves l2"></div>
          <div class="leaves l3"></div>
        </div>
      </div>
      <p class="art-title">Tropical Sunset</p>
    </div>
    
    <!-- Forest Scene -->
    <div class="art-piece forest">
      <div class="scene-container">
        <div class="forest-sky"></div>
        <div class="mountains">
          <div class="mountain m1"></div>
          <div class="mountain m2"></div>
          <div class="mountain m3"></div>
        </div>
        <div class="trees">
          <div class="tree t1">
            <div class="trunk"></div>
            <div class="foliage"></div>
          </div>
          <div class="tree t2">
            <div class="trunk"></div>
            <div class="foliage"></div>
          </div>
          <div class="tree t3">
            <div class="trunk"></div>
            <div class="foliage"></div>
          </div>
          <div class="tree t4">
            <div class="trunk"></div>
            <div class="foliage"></div>
          </div>
          <div class="tree t5">
            <div class="trunk"></div>
            <div class="foliage"></div>
          </div>
        </div>
        <div class="lake"></div>
      </div>
      <p class="art-title">Mountain Forest</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RealisticArt'
}
</script>

<style scoped>
.realistic-art-container {
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

.scene-container {
  position: relative;
  width: 500px;
  height: 300px;
  margin: 0 auto;
  overflow: hidden;
}

.art-title {
  text-align: center;
  font-size: 1.2rem;
  margin-top: 20px;
  font-weight: bold;
}

/* City Skyline */
.skyline .scene-container {
  background-color: #0a0a14;
  position: relative;
}

.sky {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 60%;
  background: linear-gradient(to bottom, #0a0a14 0%, #0c1339 40%, #1f2649 80%);
  overflow: hidden;
}

.stars {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(1px 1px at 20px 30px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 40px 70px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 50px 160px, rgba(255,255,255,0.7), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 90px 40px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 130px 80px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 160px 120px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(2px 2px at 200px 20px, rgba(255,255,255,1), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 300px 30px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 350px 60px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 400px 90px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(2px 2px at 450px 25px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 470px 120px, rgba(255,255,255,0.7), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 490px 140px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 30px 100px, rgba(255,255,255,0.7), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 120px 220px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 180px 60px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 220px 140px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 270px 100px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 330px 180px, rgba(255,255,255,0.7), rgba(0,0,0,0)),
    radial-gradient(1.5px 1.5px at 370px 120px, rgba(255,255,255,0.9), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 410px 50px, rgba(255,255,255,0.8), rgba(0,0,0,0)),
    radial-gradient(1px 1px at 450px 160px, rgba(255,255,255,0.7), rgba(0,0,0,0));
  background-repeat: repeat;
  background-size: 500px 300px;
}

.moon {
  position: absolute;
  top: 35px;
  right: 80px;
  width: 60px;
  height: 60px;
  background: radial-gradient(circle at 40% 40%, #ffffff 0%, #f0f0f0 50%, #d0d0e0 100%);
  border-radius: 50%;
  box-shadow: 0 0 25px 5px rgba(255, 255, 255, 0.8);
}

.moon::before {
  content: '';
  position: absolute;
  top: 15px;
  left: 15px;
  width: 12px;
  height: 12px;
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  filter: blur(2px);
}

.moon::after {
  content: '';
  position: absolute;
  top: 30px;
  left: 35px;
  width: 8px;
  height: 8px;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  filter: blur(1px);
}

.buildings {
  position: absolute;
  bottom: 40px;
  left: 0;
  width: 100%;
  height: 60%;
  filter: drop-shadow(0 0 15px rgba(0, 0, 0, 0.8));
}

.building {
  position: absolute;
  bottom: 0;
  background-color: transparent;
}

.b1 {
  height: 120px;
  width: 60px;
  left: 10px;
  background: linear-gradient(to bottom, #0d0d15, #111122);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b2 {
  height: 180px;
  width: 70px;
  left: 80px;
  background: linear-gradient(to bottom, #0d0d15, #121224);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b3 {
  height: 200px;
  width: 90px;
  left: 160px;
  background: linear-gradient(to bottom, #0d0d15, #131326);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b4 {
  height: 150px;
  width: 80px;
  left: 260px;
  background: linear-gradient(to bottom, #0d0d15, #121220);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b5 {
  height: 190px;
  width: 70px;
  left: 350px;
  background: linear-gradient(to bottom, #0d0d15, #111122);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b6 {
  height: 140px;
  width: 65px;
  left: 430px;
  background: linear-gradient(to bottom, #0d0d15, #101018);
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.4), 2px 0 5px rgba(0, 0, 0, 0.4);
}

.b3::before {
  content: '';
  position: absolute;
  top: -35px;
  left: 45px;
  width: 5px;
  height: 35px;
  background-color: #1a1a2e;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}

.antenna {
  position: absolute;
  top: -20px;
  left: 45px;
  width: 5px;
  height: 25px;
  background-color: #1a1a2e;
  box-shadow: 0 0 8px rgba(255, 0, 0, 0.6);
}

.antenna::after {
  content: '';
  position: absolute;
  top: -5px;
  left: 2px;
  width: 2px;
  height: 2px;
  background-color: red;
  border-radius: 50%;
  animation: blink 2s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}

.windows {
  position: absolute;
  top: 10px;
  left: 10px;
  right: 10px;
  bottom: 10px;
  background-image: 
    linear-gradient(to bottom, 
      transparent 15%, rgba(255, 230, 150, 0.7) 15%, 
      rgba(255, 230, 150, 0.7) 20%, transparent 20%,
      transparent 40%, rgba(255, 230, 150, 0.5) 40%, 
      rgba(255, 230, 150, 0.5) 45%, transparent 45%,
      transparent 65%, rgba(255, 230, 150, 0.6) 65%, 
      rgba(255, 230, 150, 0.6) 70%, transparent 70%,
      transparent 85%, rgba(255, 230, 150, 0.4) 85%, 
      rgba(255, 230, 150, 0.4) 90%, transparent 90%
    ),
    linear-gradient(to right, 
      transparent 25%, rgba(255, 230, 150, 0.6) 25%, 
      rgba(255, 230, 150, 0.6) 30%, transparent 30%,
      transparent 50%, rgba(255, 230, 150, 0.5) 50%, 
      rgba(255, 230, 150, 0.5) 55%, transparent 55%,
      transparent 75%, rgba(255, 230, 150, 0.4) 75%, 
      rgba(255, 230, 150, 0.4) 80%, transparent 80%
    );
  filter: drop-shadow(0 0 5px rgba(255, 230, 150, 0.4));
}

.b2 .windows, .b5 .windows {
  background-size: 18px 25px;
}

.b1 .windows, .b6 .windows {
  background-size: 15px 20px;
}

.b3 .windows {
  background-size: 20px 28px;
}

.b4 .windows {
  background-size: 17px 23px;
}

.ground {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 40px;
  background: linear-gradient(to bottom, #0a0a12, #080810);
  box-shadow: 0 -5px 15px rgba(0, 0, 0, 0.6);
}

.ground::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 1px;
  background: linear-gradient(to right, 
    transparent, rgba(255, 230, 150, 0.3), 
    rgba(255, 230, 150, 0.5), rgba(255, 230, 150, 0.3), 
    transparent
  );
}

/* Sunset Beach */
.sunset-beach .scene-container {
  background-color: #1a1a1a;
}

.sunset-sky {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 70%;
  background: linear-gradient(to bottom, 
    #051f2e 0%,
    #1e3c5a 10%, 
    #b84027 30%, 
    #f07e3c 45%, 
    #fdb86b 60%, 
    #fff0d4 75%);
  overflow: hidden;
}

.sunset-sky::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    ellipse at center,
    rgba(253, 184, 107, 0.2) 0%,
    rgba(253, 184, 107, 0.1) 40%,
    rgba(0, 0, 0, 0) 70%
  );
}

.sun {
  position: absolute;
  width: 80px;
  height: 80px;
  background: radial-gradient(
    circle at center,
    #ffffff 0%,
    #fff176 20%,
    #ff9800 40%,
    #ff5722 60%,
    #d84315 80%,
    #bf360c 100%
  );
  border-radius: 50%;
  top: 45%;
  right: 80px;
  transform: translateY(-50%);
  box-shadow: 0 0 60px rgba(255, 87, 34, 0.8);
  filter: blur(1px);
}

.sun::after {
  content: '';
  position: absolute;
  top: -10px;
  left: -10px;
  right: -10px;
  bottom: -10px;
  border-radius: 50%;
  background: radial-gradient(
    circle at center,
    rgba(255, 255, 255, 0.4) 0%,
    rgba(255, 255, 255, 0.1) 60%,
    rgba(255, 255, 255, 0) 70%
  );
}

.ocean {
  position: absolute;
  bottom: 50px;
  left: 0;
  width: 100%;
  height: 30%;
  background: linear-gradient(to bottom, 
    #063852 0%, 
    #085980 40%, 
    #0c7bb3 70%, 
    #1597dc 100%);
  overflow: hidden;
}

.ocean::before {
  content: '';
  position: absolute;
  width: 200%;
  height: 100%;
  top: -10%;
  left: -50%;
  background: radial-gradient(
    ellipse at center,
    rgba(255, 197, 148, 0.4) 0%,
    rgba(255, 197, 148, 0.2) 50%,
    rgba(255, 197, 148, 0) 70%
  );
  filter: blur(3px);
}

.wave {
  position: absolute;
  height: 20px;
  width: 120%;
  left: -10%;
  background-color: transparent;
  border-radius: 100%;
  opacity: 0.8;
}

.w1 {
  bottom: 15px;
  height: 25px;
  background: linear-gradient(to bottom, 
    rgba(255, 255, 255, 0.2) 0%,
    rgba(64, 164, 223, 0.4) 100%);
  animation: wave 8s linear infinite;
}

.w2 {
  bottom: 5px;
  height: 15px;
  background: linear-gradient(to bottom, 
    rgba(255, 255, 255, 0.3) 0%,
    rgba(64, 164, 223, 0.5) 100%);
  animation: wave 6s linear infinite;
  animation-delay: 1s;
}

.w3 {
  bottom: -5px;
  height: 10px;
  background: linear-gradient(to bottom, 
    rgba(255, 255, 255, 0.4) 0%,
    rgba(64, 164, 223, 0.6) 100%);
  animation: wave 4s linear infinite;
  animation-delay: 2s;
}

@keyframes wave {
  0% {
    transform: translateX(0) scaleY(1);
  }
  50% {
    transform: translateX(-25px) scaleY(0.8);
  }
  100% {
    transform: translateX(0) scaleY(1);
  }
}

.beach {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 50px;
  background: linear-gradient(to bottom, 
    #e8c39e 0%, 
    #ddb185 50%, 
    #c19a6b 100%);
}

.beach::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: linear-gradient(to bottom,
    rgba(16, 151, 220, 0.3) 0%,
    rgba(232, 195, 158, 0.6) 100%);
  filter: blur(1px);
}

.palm-tree {
  position: absolute;
  bottom: 50px;
  left: 80px;
  z-index: 10;
  transform-origin: bottom left;
  transform: scale(0.9);
}

.palm-tree .trunk {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 15px;
  height: 80px;
  background: linear-gradient(
    to right,
    #513823 0%,
    #8b5a2b 25%,
    #a0522d 50%,
    #8b5a2b 75%,
    #513823 100%
  );
  transform: skewX(-8deg);
  border-radius: 40% 40% 5% 5% / 5% 5% 5% 5%;
}

.palm-tree .trunk::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    to bottom,
    transparent,
    transparent 10px,
    rgba(0, 0, 0, 0.05) 10px,
    rgba(0, 0, 0, 0.05) 20px
  );
}

.palm-tree .leaves {
  position: absolute;
  border-radius: 0 100% 0 100%;
  background: linear-gradient(
    to bottom right,
    #2e7d32 0%,
    #1b5e20 100%
  );
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.4);
  transform-origin: bottom left;
}

.palm-tree .l1 {
  width: 70px;
  height: 30px;
  top: -20px;
  left: -10px;
  transform: rotate(-20deg);
  filter: brightness(1.1);
}

.palm-tree .l2 {
  width: 65px;
  height: 35px;
  top: -30px;
  left: -35px;
  transform: rotate(-60deg);
  filter: brightness(0.9);
}

.palm-tree .l3 {
  width: 70px;
  height: 30px;
  top: -35px;
  left: 5px;
  transform: rotate(20deg);
  filter: brightness(1.05);
}

.palm-tree .l1::after, .palm-tree .l2::after, .palm-tree .l3::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    to bottom right,
    rgba(255, 255, 255, 0.1) 0%,
    rgba(0, 0, 0, 0.1) 100%
  );
  border-radius: inherit;
}

/* Forest Scene - Enhanced Photorealism */
.forest .scene-container {
  background-color: #c8e6ff;
}

.forest-sky {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, 
    #5d8cb3 0%,
    #81a8c7 30%, 
    #a6c5e1 60%, 
    #c8e6ff 100%);
  overflow: hidden;
}

.forest-sky::before {
  content: '';
  position: absolute;
  top: 10px;
  right: 80px;
  width: 60px;
  height: 60px;
  background: radial-gradient(
    circle at center,
    rgba(255, 255, 255, 0.9) 0%,
    rgba(255, 255, 255, 0.6) 40%,
    rgba(255, 255, 255, 0) 70%
  );
  filter: blur(5px);
}

.mountains {
  position: absolute;
  bottom: 100px;
  width: 100%;
  height: 150px;
}

.mountain {
  position: absolute;
  bottom: 0;
  background: linear-gradient(to bottom, transparent 0%, transparent 60%, rgba(0, 0, 0, 0.1) 100%);
}

.m1 {
  left: -50px;
  width: 280px;
  height: 150px;
  background: linear-gradient(145deg, #9ba9b4 0%, #8b97a3 40%, #6d7986 100%);
  clip-path: polygon(50% 0%, 100% 100%, 0% 100%);
  transform: scaleX(1.2);
  opacity: 0.85;
}

.m2 {
  left: 100px;
  width: 320px;
  height: 160px;
  background: linear-gradient(145deg, #8c9aa6 0%, #7b8997 40%, #5a6675 100%);
  clip-path: polygon(50% 0%, 100% 100%, 0% 100%);
  transform: scaleX(1.1);
  z-index: 2;
}

.m3 {
  right: -50px;
  width: 300px;
  height: 140px;
  background: linear-gradient(215deg, #a7b5c0 0%, #939fa9 40%, #768088 100%);
  clip-path: polygon(50% 0%, 100% 100%, 0% 100%);
  transform: scaleX(1.15);
  z-index: 1;
}

.m1::after, .m2::after, .m3::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, 
    rgba(255, 255, 255, 0.05) 0%,
    rgba(255, 255, 255, 0) 40%,
    rgba(0, 0, 0, 0.1) 100%
  );
  clip-path: inherit;
}

.m2::before {
  content: '';
  position: absolute;
  top: 20px;
  left: 50%;
  width: 100px;
  height: 50px;
  background: linear-gradient(to bottom, #fff 0%, rgba(255, 255, 255, 0) 100%);
  transform: translateX(-50%) rotate(-5deg);
  filter: blur(20px);
  opacity: 0.3;
}

.trees {
  position: absolute;
  bottom: 40px;
  width: 100%;
  z-index: 3;
}

.tree {
  position: absolute;
  bottom: 0;
}

.tree .trunk {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 12px;
  height: 35px;
  background: linear-gradient(to right, 
    #3e2723 0%,
    #5d4037 50%,
    #3e2723 100%
  );
  border-radius: 2px 2px 4px 4px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.3);
}

.tree .foliage {
  position: absolute;
  bottom: 25px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 80px;
  background: linear-gradient(to bottom,
    #1b5e20 0%,
    #2e7d32 50%,
    #1b5e20 100%
  );
  clip-path: polygon(50% 0%, 20% 40%, 0% 100%, 100% 100%, 80% 40%);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.t1 {
  left: 50px;
  bottom: 0;
  z-index: 3;
  transform: scale(0.9);
}

.t1 .foliage {
  background: linear-gradient(to bottom,
    #1b5e20 0%,
    #205723 50%,
    #154a19 100%
  );
  filter: brightness(0.9);
}

.t2 {
  left: 120px;
  bottom: 5px;
  z-index: 4;
  transform: scale(1.1);
}

.t2 .foliage {
  background: linear-gradient(to bottom,
    #2e7d32 0%,
    #388e3c 50%,
    #2e7d32 100%
  );
  filter: brightness(1.05);
}

.t3 {
  left: 200px;
  bottom: 0;
  z-index: 5;
  transform: scale(1);
}

.t3 .foliage {
  background: linear-gradient(to bottom,
    #388e3c 0%,
    #43a047 50%,
    #388e3c 100%
  );
  filter: brightness(1.1);
}

.t4 {
  left: 280px;
  bottom: -5px;
  z-index: 6;
  transform: scale(0.95);
}

.t4 .foliage {
  background: linear-gradient(to bottom,
    #2e7d32 0%,
    #388e3c 50%,
    #2e7d32 100%
  );
  filter: brightness(0.95);
}

.t5 {
  left: 380px;
  bottom: 0;
  z-index: 7;
  transform: scale(1.05);
}

.t5 .foliage {
  background: linear-gradient(to bottom,
    #1b5e20 0%,
    #2e7d32 50%,
    #1b5e20 100%
  );
  filter: brightness(1);
}

.tree .foliage::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at top,
    rgba(255, 255, 255, 0.1) 0%,
    rgba(255, 255, 255, 0) 70%
  );
  clip-path: inherit;
}

.lake {
  position: absolute;
  bottom: 0;
  left: 40px;
  width: 420px;
  height: 40px;
  background: linear-gradient(to bottom, 
    #4fc3f7 0%, 
    #29b6f6 40%, 
    #039be5 100%
  );
  border-radius: 50% / 20%;
  box-shadow: inset 0 5px 10px rgba(0, 0, 0, 0.2);
  overflow: hidden;
}

.lake::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg,
    rgba(255, 255, 255, 0.1) 0%,
    rgba(255, 255, 255, 0.3) 50%,
    rgba(255, 255, 255, 0.1) 100%
  );
  animation: shimmer 10s infinite linear;
}

.lake::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    45deg,
    rgba(255, 255, 255, 0.05),
    rgba(255, 255, 255, 0.05) 10px,
    transparent 10px,
    transparent 20px
  );
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%) skewX(45deg);
  }
  100% {
    transform: translateX(100%) skewX(45deg);
  }
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .scene-container {
    width: 300px;
    height: 200px;
    transform: scale(0.8);
    transform-origin: center top;
  }
}
</style>