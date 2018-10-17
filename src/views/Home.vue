<template>

  <div class="wrapper">
    <header class="header">
      
    </header>
    <main class="main">
      <div class="memoram">
        <div v-for="index in imagePositions" @click="handleClick(items[index],index)" :key="index" :class="{'memoram__item':true,'player-1':items[index].player===2?true:false,'player-2':items[index].player===1?true:false}">
          <img class="memoram__item__img" :src="items[index].isClicked? getImage(items[index].image):require('../assets/logo.png')" alt=""/>
        </div>
      </div>

    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import { setTimeout } from "timers";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  created() {
    this.generateRandom();
    // console.log(this.generateRandom());
  },

  data() {
    return {
      turnCount: 1,
      select: 0,
      score: 0,
      imagePositions: [],
      currentSelect: null,
      lastSelect: null,
      clicks: 0,
      items: [
        { id: 1, image: "img1.png", isClicked: false, player: 0 },
        { id: 2, image: "img1.png", isClicked: false, player: 0 },
        { id: 3, image: "img2.png", isClicked: false, player: 0 },
        { id: 4, image: "img2.png", isClicked: false, player: 0 },
        { id: 5, image: "img3.png", isClicked: false, player: 0 },
        { id: 6, image: "img3.png", isClicked: false, player: 0 },
        { id: 7, image: "img4.png", isClicked: false, player: 0 },
        { id: 8, image: "img4.png", isClicked: false, player: 0 },
        { id: 9, image: "img5.png", isClicked: false, player: 0 },
        { id: 10, image: "img5.png", isClicked: false, player: 0 },
        { id: 11, image: "img6.png", isClicked: false, player: 0 },
        { id: 12, image: "img6.png", isClicked: false, player: 0 },
        { id: 13, image: "img7.png", isClicked: false, player: 0 },
        { id: 14, image: "img7.png", isClicked: false, player: 0 },
        { id: 15, image: "img8.png", isClicked: false, player: 0 },
        { id: 16, image: "img8.png", isClicked: false, player: 0 }
      ]
    };
  },
  methods: {
    reset() {
      this.lastSelect = null;
      this.currentSelect = null;
    },
    checkImages() {
      if (this.currentSelect.image === this.lastSelect.image) {
        this.score++;
        this.items[this.currentSelect.index].player =
          this.turnCount % 2 === 0 ? 2 : 1;
        this.items[this.lastSelect.index].player =
          this.turnCount % 2 === 0 ? 2 : 1;
        this.reset();
      } else {
        this.turnCount++;
        setTimeout(() => {
          this.items[this.currentSelect.index].isClicked = false;
          this.items[this.lastSelect.index].isClicked = false;
          this.reset();
        }, 400);
      }
    },

    handleClick(item, index) {
      if (item.player === 0) {
        this.clicks++;
        switch (this.clicks) {
          case 1: {
            item.isClicked = true;
            this.currentSelect = { ...item, index };
            break;
          }
          case 2: {
            this.clicks = 0;
            item.isClicked = true;

            this.lastSelect = { ...item, index };
            this.checkImages();
            // this.turnCount++;

            break;
          }
        }
        console.log(`${item.id} was pressed!`);
      }
      // this.clickCount();
    },
    getImage(img) {
      return require(`../assets/${img}`);
    },
    generateRandom() {
      let imagePositions = [];
      while (imagePositions.length < 16) {
        let num = Math.floor(Math.random() * 16);
        if (!imagePositions.includes(num)) imagePositions.push(num);
      }
      this.imagePositions = imagePositions;
      // return imagePosition;
      // for(let i=0; i<16;i++)
    }
  }
};
</script>

<style lang="scss">
.wrapper {
  display: grid;
  grid-template-rows: 0.1fr 0.9fr;
  height: 100vh;
}

.main {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f2f2f2;
}
.memoram {
  display: grid;
  // margin-top: 150px;
  padding: 5px;
  background: rgba(gray, 0.1);
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(4, 1fr);
  grid-gap: 5px;
  width: 500px;
  height: 500px;

  &__item {
    background: #fff;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    transition: all ease 0.3s;
    &.player-1 {
      background: red;
    }
    &.player-2 {
      background: blue;
    }
    &__img {
      $s: 100px;
      display: block;
      width: $s;
      height: $s;
    }
    &:hover {
      transform: scale(1.4);
      // background: yellow;
    }
  }
}
</style>

