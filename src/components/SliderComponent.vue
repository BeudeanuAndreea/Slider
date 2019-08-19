<template>
  <div class="container">
    <div class="carousel">
      <div class="images">
        <div v-for="(img,index) in imageArray" :key="index">
          <img class="image" ref="index" :src="img.src" />
        </div>
      </div>
    </div>
    <font-awesome-icon class="arrow arrow-left" icon="chevron-left" v-on:click="moveLeft"></font-awesome-icon>
    <font-awesome-icon class="arrow arrow-right" icon="chevron-right" v-on:click="moveRight"></font-awesome-icon>
  </div>
</template>

<script>
import TweenMax from "gsap/TweenMax";
import { TimelineLite, CSSPlugin, AttrPlugin } from "gsap/all";

var image_1 = require("../assets/1.jpg");
var image_2 = require("../assets/2.jpg");
var image_3 = require("../assets/3.jpg");
var image_4 = require("../assets/4.jpg");
var image_5 = require("../assets/5.jpg");
var image_6 = require("../assets/6.jpg");
var image_7 = require("../assets/7.jpg");
var image_8 = require("../assets/8.jpg");
var image_9 = require("../assets/9.jpg");
var image_10 = require("../assets/10.jpg");

export default {
  data() {
    return {
      position: 0,
      position2: 1,
      imageArray: [
        { src: image_1 },
        { src: image_2 },
        { src: image_3 },
        { src: image_4 },
        { src: image_5 },
        { src: image_6 },
        { src: image_7 },
        { src: image_8 },
        { src: image_9 },
        { src: image_10 }
      ]
    };
  },
  mounted() {
    const tl = new TimelineLite();
    TweenMax.to(".images :nth-child(2) .image", 1, {
      opacity: 1
    });
  },
  methods: {
    move() {
      const tl = new TimelineLite();
      let value = this.position * 50;
      value = value * -1;
      tl.to(".carousel", 1, {
        x: `${value}%`
      });
      var imgM = this.$refs.index[this.position + 1];
      var imgR = this.$refs.index[this.position];
      var imgL = this.$refs.index[this.position + 2];
      TweenMax.to(imgM, 1, {
        opacity: 1
      });
      imgR &&
        TweenMax.to(imgR, 1, {
          opacity: 0.2
        });
      imgL &&
        TweenMax.to(imgL, 1, {
          opacity: 0.2
        });
    },

    moveRight() {
      if (this.position != this.imageArray.length - 2) {
        this.position++;
      }
      if (this.position > -1) {
        TweenMax.to(".arrow-left", 1, {
          opacity: 1,
          display: ""
        });
      }
      if (this.position == this.imageArray.length - 2) {
        TweenMax.to(".arrow-right", 1, {
          opacity: 0,
          display: "none"
        });
      }
      this.move();
    },
    moveLeft() {
      if (this.position != -1) {
        this.position--;
      }
      if (this.position == -1) {
        TweenMax.to(".arrow-left", 1, {
          opacity: 0,
          display: "none"
        });
      }
      if (this.position < this.imageArray.length - 2) {
        TweenMax.to(".arrow-right", 1, {
          opacity: 1,
          display: ""
        });
      }
      this.move();
    }
  }
};
</script>

<style >
body {
  margin: 0;
}

.container {
  overflow: hidden;
  position: relative;
}

.carousel {
  width: 100%;
}

.images {
  display: flex;
  transform: translateX(-150px);
  overflow: visible;
}

.images > * {
  margin-right: calc(50% - 300px);
  box-sizing: border-box;
}

.image {
  display: block;
  width: 300px;
  height: 300px;
  opacity: 0.3;
}

.arrow {
  position: absolute;
  top: 50%;
  cursor: pointer;
  transform: translateY(-50%);
  font-size: 40px;
  color: black;
  padding: 10px;
}

.arrow-left {
  left: 140px;
}

.arrow-right {
  right: 140px;
}
</style>

