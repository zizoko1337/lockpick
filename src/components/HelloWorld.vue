<template>
  <div class="hello">
    <div class="openingBar " v-show="!loaded && showBar">
      <p class="text ">Picking Lock...</p>
    </div>

    <div class="box" v-show="loaded">
      <img class="imgA1" src="../assets/lockpick.png">
      <img ref="myImage2" class="imgB1" src="../assets/correct.png">
      <img ref="myImage3" class="imgB1" src="../assets/incorrect.png">
      <img ref="myImage" class="imgB2" src="../assets/line.png">
    </div>
  <button class="btn" v-if="!showBar" @click="rotate360ccw(); rotateRandomAngle(); startTask(); showBar = true">Start Opening</button>
  <button class="btn" v-if="showBar" @click="reloadPage">Try Again</button>


  </div>
</template>

<script>
export default {
  data() {
    return {
      animationId: null,
      isRotating: false,
      lastAngle: 0,
      correctAngles: null,
      incorrectAngles: null,
      lastTimestamp: 0,
      canRandomRotate: true,
      loaded: false,
      showBar: false
    };
  },
  methods: {

    async startTask() {
      const delay = Math.random() * (3500 - 2000) + 2000; // Random delay between 2 and 3.5 seconds in milliseconds
      await this.delay(delay); // Wait for the specified delay
      this.loaded = true;

      this.rotate360ccw(); // Call the method to perform the task
    },
    async delay(ms) {
      return new Promise(resolve => setTimeout(resolve, ms)); // Wait for the specified number of milliseconds
    },


    rotate360ccw() {
      const image = this.$refs.myImage;
      let angle = this.lastAngle || 0;
      const duration = Math.floor(Math.random() * 400) + 600; // random duration between 500 and 1000 milliseconds
      const start = performance.now() - (this.lastTimestamp || 0);
      this.isRotating = true;

      const rotate = (timestamp) => {
        const elapsed = timestamp - start;
        const progress = elapsed / duration;
        angle = this.lastAngle + progress * 360;

        if (angle <= 360 && this.isRotating) {
          image.style.transform = `rotate(${360 - angle}deg)`;
          this.animationId = window.requestAnimationFrame(rotate);
        }
      };

      this.animationId = window.requestAnimationFrame(rotate);
    },
    stopRotation() {
      this.isRotating = false;
      window.cancelAnimationFrame(this.animationId);
      const image = this.$refs.myImage;
      const style = window.getComputedStyle(image);
      const transform = style.getPropertyValue('transform');
      const matrix = transform.slice(7, -1).split(', ');
      const angle = Math.round(Math.atan2(matrix[1], matrix[0]) * (180 / Math.PI));
      this.lastAngle = angle < 0 ? angle + 360 : angle;
      this.lastTimestamp = performance.now() - this.lastAngle * 1000 / 360;
      console.log( this.lastAngle)
        console.log( this.correctAngles)
        console.log( this.incorrectAngles)
    },
    rotateRandomAngle() {
      if(this.canRandomRotate){
        const correct = this.$refs.myImage2;
        const incorrect = this.$refs.myImage3;
        const randomAngleCorrect = Math.floor(Math.random() * 101) + 100; // Random angle between 100 and 200 degrees
        const randomAngleIncorrect = randomAngleCorrect + Math.floor(Math.random() * -30) - 15; 
        correct.style.transform = `rotate(${randomAngleCorrect}deg)`;
        incorrect.style.transform = `rotate(${randomAngleIncorrect}deg)`;
        this.correctAngles = {start: randomAngleCorrect ,stop: randomAngleCorrect + 46};
        this.incorrectAngles = {start: randomAngleIncorrect ,stop: randomAngleIncorrect + 4};
      }
      this.canRandomRotate = false;
    },
    reloadPage() {
      window.location.reload();
    }
  },
  mounted() {

    this.rotate360ccw();
    document.addEventListener('keydown', (event) => {
      if (event.code === 'Space') {
        this.stopRotation();
      }
    });
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

img {
  position: absolute;
}


.imgA1 {
  z-index: 1;
}
.imgB1 {
  z-index: 3;
}
.imgB2 {
  z-index: 5;
}

.box {
  background-color: black;
  position: absolute;
  left: 50%;
  top: 60%;
  margin-left: -175px;
  /* -1/2 width */
  margin-top: -175px;
  /* -1/2 height */
}
.openingBar{
  position: absolute;
  left: 50%;
  top: 80%;
  margin-left: -175px;
  width: 350px;
  height: 50px;
  border: solid black 5px;
  background-color: #ccc;
  overflow: hidden;
}
.openingBar:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 0%;
  background: rgb(37,38,0);
background: linear-gradient(90deg, rgba(37,38,0,0.7371323529411764) 0%, rgba(252,255,106,0.3309698879551821) 50%, rgba(37,38,0,1) 100%);  transition: width 4s ease-in-out;
  animation: fill 4s ease-in-out;
}

.btn {
  height: 60px;
  width: 200px;
}

  .text{
    color: black;
    font-size: 20px
  }


  @keyframes fill {
  0% {
    width: 0%;
  }
  100% {
    width: 100%;
  }


}
</style>
