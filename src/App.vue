<template>
  <div class="app-head">
    <h1>Etch-a-sketch</h1>
  </div>

  <div class="body-app">

    <div class="choices">
      <div class="color">
        <input type="color" name="" id="color-id" v-model="selectedColor">
      </div>
      <div class="Color Mode">
        <button @click="chooseColorMode()">Color Mode</button>
      </div>
      <div class="Rainbow Mode">
        <button @click="chooseRainbow()">Rainbow Mode</button>
      </div>
      <div class="Eraser">
        <button @click="chooseErase()">Eraser</button>
      </div>
      <div class="Clear">
        <button @click="clear()">Clear</button>
      </div>
    </div>

    <div class="main">
      <div class="app-divs" v-for="item in divList" :key="item.index" :style="{ backgroundColor: item.color }"
        @click="isDown = !isDown"  @mouseover="changeColor(item.index)">
        <div style="width: 10px;height: 10px"></div>
      </div>
      <footer>
        <div style="margin-bottom: 4px;">
          Created by Caner
        </div>
        <div>
          <a :href="githubURL" target="_blank"><img src="@/assets/github-icon.png" alt="github-icon"></a>
        </div>
        </footer>
    </div>

</div>
</template>

<script>


export default {
  data() {
    return {
      check: false,
      divList: [],
      selectedColor: "#212121",
      isRainbow: false,
      isErase: false,
      isDown: false,
      githubURL : "https://github.com/canertunc",

    }
  },
  created() {
    for (let i = 0; i < 2500; i++) {
      this.divList.push({ content: 'div', color: '#ffff', index: i });
    }
  },
  methods: {
    changeColor(index) {
      if (this.isDown) {
        if (!this.isRainbow) {
          if (!this.isErase) {
            this.divList[index].color = this.selectedColor;
          } else {
            this.divList[index].color = "#ffff";

          }
        } else {
          let rainbowColor = this.getRainbowColors(Math.floor(Math.random() * 360));
          this.divList[index].color = rainbowColor;
        }
      }

    },
    chooseErase() {
      this.isRainbow = false;
      this.isErase = true;
      this.isDown = false;

    },
    chooseRainbow() {
      this.isRainbow = true;
      this.isDown = false;

    },
    getRainbowColors(hue) {
      var colors = [];
      var saturation = 100;
      var lightness = 50;
      var color = 'hsl(' + hue + ', ' + saturation + '%, ' + lightness + '%)';
      colors.push(color);
      return colors;
    },
    chooseColorMode() {
      this.isRainbow = false
      this.isErase = false
    },
    clear() {
      for (let i = 0; i < 2500; i++) {
        this.divList[i].color = "#ffff";
        this.isDown = false;
      }
    },

  }
}
</script>

<style>
@keyframes fade {
  0% { color: rgb(223, 14, 14);;}
  50% { color: blue; }
  100% { color: rgb(223, 14, 14); }
}
.app-head h1 {
  animation: fade 5s infinite;
}

</style>
