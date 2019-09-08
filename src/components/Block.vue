<template>
  <div
    :class="{'block-open': isOpenBlock, 'disabled': isDisabled}"
    @click="openBlock"
    :data-img="imagePath"
  >
    <img :src="imagePath" :alt="imagePath" width="100%" />
  </div>
</template>

<script>
import { setTimeout } from "timers";

let opennedBlocks = [];

export default {
  data() {
    return {
      isOpenBlock: false,
      isUnactive: false,
      isDisabled: false,
      blockStyle: {
        height: 0,
        margin: 0,
        width: 0
      }
    };
  },
  props: {
    index: Number,
    settings: {
      type: Object
    },
    imagePath: String
  },
  methods: {
    openBlock(event) {
      if (this.isUnactive) {
        return;
      }

      if (opennedBlocks.length < 2) {
        this.isOpenBlock = true;
        this.isUnactive = true;
        opennedBlocks.push(this);
      } else {
        return false;
      }
      this.checkBlocks();
    },
    checkBlocks() {
      if (opennedBlocks.length == 2) {
        setTimeout(function() {
          if (
            opennedBlocks[0].$el.dataset.img == opennedBlocks[1].$el.dataset.img
          ) {
            opennedBlocks.forEach(el => {
              el.$data.isOpenBlock = false;
              el.$data.isDisabled = true;
            });
          } else {
            opennedBlocks.forEach(el => {
              el.$data.isOpenBlock = false;
              el.$data.isUnactive = false;
            });
          }
          opennedBlocks = [];
        }, 1000);
      }
    }
  }
};
</script>

<style scoped>
div {
  background-color: #dcf3ec;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  border: 1px solid #8fb3a8;
  border-radius: 3px;
  cursor: pointer;
  height: 50px;
  margin: 3px;
  opacity: 0.75;
  user-select: none;
  transform: rotateY(-180deg);
  transition: all 0.25s ease-in-out;
  width: 50px;
}

div:hover {
  opacity: 1;
}

img {
  opacity: 0;
  pointer-events: none;
  transition: opacity 0s ease-in-out;
  transition-delay: 0.125s;
}

div.block-open {
  opacity: 1;
  transform: translateY(0);
  transition: all 0.25s ease-in-out;
}

div.disabled {
  background-color: #dadada;
  cursor: default;
  pointer-events: none;
}

div.block-open img {
  opacity: 1;
  transition: opacity 0.1s ease-in-out;
  transition-delay: 0.125s;
}
</style>