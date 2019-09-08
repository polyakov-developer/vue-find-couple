<template>
  <div class="container">
    <app-playground-area :settings="settings.area">
      <!-- :settings="settings.block" -->
      <app-block v-for="(item, index) of arrayItems" :imagePath="item" :key="index"></app-block>
    </app-playground-area>
  </div>
</template>

<script>
import PlaygroundArea from "./components/PlaygroundArea.vue";
import Block from "./components/Block.vue";

// Перемешать изображения
const shuffle = function(arr) {
  var j, temp;
  for (var i = arr.length - 1; i > 0; i--) {
    j = Math.floor(Math.random() * (i + 1));
    temp = arr[j];
    arr[j] = arr[i];
    arr[i] = temp;
  }
  return arr;
};

let imagesArr = [
  "../img/1.png",
  "../img/2.png",
  "../img/3.png",
  "../img/4.png",
  "../img/5.png",
  "../img/6.png",
  "../img/7.png",
  "../img/8.png"
];

let arr = imagesArr.slice(0, imagesArr.length).concat(imagesArr);

arr = shuffle(arr);

export default {
  data() {
    return {
      arrayItems: arr,
      settings: {
        area: {
          size: 16,
          width: 0,
          height: 0
        },
        block: {
          image: "path.png",
          height: 50,
          gutter: 3,
          width: 50
        }
      }
    };
  },
  components: {
    "app-playground-area": PlaygroundArea,
    "app-block": Block
  },
  created() {
    this.settings.area.width =
      Math.sqrt(this.settings.area.size) *
      (this.settings.block.width + this.settings.block.gutter * 4);
    this.settings.area.height =
      Math.sqrt(this.settings.area.size) *
      (this.settings.block.height * this.settings.block.gutter);
  }
};
</script>

<style scoped>
.container {
  display: flex;
  height: 100vh;
  margin: 0 auto;
  max-width: 700px;
  width: 100%;
}
</style>