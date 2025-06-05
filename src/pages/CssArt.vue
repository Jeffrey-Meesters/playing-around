<template>
  <div class="css-art-container">
    <h1>Abstract CSS Art Gallery</h1>
    
    <!-- Mondrian-inspired composition -->
    <div class="art-piece mondrian">
      <div class="mondrian-container">
        <div class="red-square"></div>
        <div class="blue-rect"></div>
        <div class="yellow-square"></div>
        <div class="white-rect-1"></div>
        <div class="white-rect-2"></div>
        <div class="black-lines"></div>
      </div>
      <p class="art-title">Mondrian Composition</p>
    </div>
    
    <!-- Kandinsky-inspired circles -->
    <div class="art-piece kandinsky">
      <div class="kandinsky-container">
        <div class="circle circle-1"></div>
        <div class="circle circle-2"></div>
        <div class="circle circle-3"></div>
        <div class="circle circle-4"></div>
        <div class="circle circle-5"></div>
        <div class="line line-1"></div>
        <div class="line line-2"></div>
        <div class="line line-3"></div>
      </div>
      <p class="art-title">Kandinsky Circles</p>
    </div>
    
    <!-- Rothko-inspired color fields -->
    <div class="art-piece rothko">
      <div class="rothko-container">
        <div class="color-field field-1"></div>
        <div class="color-field field-2"></div>
        <div class="color-field field-3"></div>
      </div>
      <p class="art-title">Rothko Color Fields</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CssArt'
}
</script>

<style scoped>
.css-art-container {
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
  font-size: 1.2rem;
  margin-top: 20px;
  font-weight: bold;
}

/* Mondrian-inspired art */
.mondrian-container {
  position: relative;
  width: 400px;
  height: 400px;
  margin: 0 auto;
  background-color: #000;
  padding: 10px;
}

.mondrian-container div {
  position: absolute;
}

.red-square {
  top: 10px;
  left: 10px;
  width: 120px;
  height: 120px;
  background-color: #e42f2f;
}

.blue-rect {
  top: 10px;
  right: 10px;
  width: 80px;
  height: 180px;
  background-color: #2f54e4;
}

.yellow-square {
  bottom: 10px;
  left: 200px;
  width: 100px;
  height: 100px;
  background-color: #ffde2f;
}

.white-rect-1 {
  top: 10px;
  left: 140px;
  width: 170px;
  height: 120px;
  background-color: #fff;
}

.white-rect-2 {
  top: 140px;
  left: 10px;
  width: 280px;
  height: 250px;
  background-color: #fff;
}

.black-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 10px solid #000;
  box-sizing: border-box;
  pointer-events: none;
  z-index: 10;
}

.black-lines::before, .black-lines::after {
  content: '';
  position: absolute;
  background-color: #000;
}

.black-lines::before {
  top: 130px;
  left: 0;
  width: 100%;
  height: 10px;
}

.black-lines::after {
  top: 0;
  left: 130px;
  width: 10px;
  height: 100%;
}

/* Kandinsky-inspired art */
.kandinsky-container {
  position: relative;
  width: 400px;
  height: 400px;
  margin: 0 auto;
  background-color: #f2f0e6;
}

.kandinsky-container .circle {
  position: absolute;
  border-radius: 50%;
}

.circle-1 {
  width: 120px;
  height: 120px;
  top: 50px;
  left: 50px;
  background-color: #e42f2f;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.circle-2 {
  width: 80px;
  height: 80px;
  top: 100px;
  left: 200px;
  background-color: #2f54e4;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.circle-3 {
  width: 150px;
  height: 150px;
  top: 200px;
  left: 80px;
  background-color: #ffde2f;
  opacity: 0.8;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.circle-4 {
  width: 60px;
  height: 60px;
  top: 150px;
  left: 300px;
  background-color: #4caf50;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.circle-5 {
  width: 90px;
  height: 90px;
  top: 250px;
  left: 250px;
  background-color: #9c27b0;
  opacity: 0.7;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.kandinsky-container .line {
  position: absolute;
  background-color: #000;
}

.line-1 {
  width: 3px;
  height: 200px;
  top: 50px;
  left: 180px;
  transform: rotate(45deg);
}

.line-2 {
  width: 3px;
  height: 150px;
  top: 120px;
  left: 300px;
  transform: rotate(-30deg);
}

.line-3 {
  width: 3px;
  height: 180px;
  top: 220px;
  left: 100px;
  transform: rotate(15deg);
}

/* Rothko-inspired art */
.rothko-container {
  position: relative;
  width: 400px;
  height: 400px;
  margin: 0 auto;
  background-color: #262626;
  padding: 20px;
  box-sizing: border-box;
}

.rothko-container .color-field {
  margin: 0 auto;
  width: 85%;
  position: relative;
  border-radius: 2px;
}

.field-1 {
  height: 35%;
  background-color: #9e392b;
  margin-bottom: 20px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.4) inset;
}

.field-2 {
  height: 30%;
  background-color: #c25c12;
  margin-bottom: 20px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.4) inset;
}

.field-3 {
  height: 20%;
  background-color: #e89b00;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.4) inset;
}

/* Make the art responsive */
@media (max-width: 500px) {
  .mondrian-container,
  .kandinsky-container,
  .rothko-container {
    width: 300px;
    height: 300px;
  }
  
  /* Adjust positions proportionally */
  .circle-1, .circle-2, .circle-3, .circle-4, .circle-5,
  .line-1, .line-2, .line-3,
  .red-square, .blue-rect, .yellow-square, .white-rect-1, .white-rect-2 {
    transform: scale(0.75);
  }
}
</style>