<template>
  <div>
    <div class="die-icon" :style="dieStyle">
      <img :width="width" :height="height" :src="getImgUrl()" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      color: "dark",
    };
  },
  props: {
    id: {
      type: Number,
      default: 1,
    },
    number: {
      type: Number,
      default: 3,
    },
    width: {
      type: [Number, String],
      default: 64,
    },
    height: {
      type: [Number, String],
      default: 64,
    },
    left: {
      type: Number,
      default: 10,
    },

    top: {
      type: Number,
      default: 10,
    },

    rotate: {
      type: Number,
      default: 10,
    },
  },
  methods: {
    getImgUrl() {
      return require("../assets/Dice/die-" +
        this.number +
        "-" +
        this.dieColor +
        ".svg");
    },
  },
  computed: {
    dieStyle() {
      return {
        left: `${this.left}%`,
        top: `${this.top}%`,
        transform: `rotate(${this.rotate}deg)`,
      };
    },
    dieColor() {
      switch (this.id) {
        case 1:
          return "dark";
        case 2:
          return "white";
        case 3:
          return "dark";
        case 4:
          return "white";
        case 5:
          return "dark";
        default:
          return "white";
      }
    },
  },
};
</script>

<style scoped>
.die-icon {
  position: absolute;
  transition: top 1s, left 1s, transform 1s;
}
</style>
