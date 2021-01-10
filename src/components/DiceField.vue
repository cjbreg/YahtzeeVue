<template>
  <div>
    <div class="field">
      <div v-for="die in dice" :key="die.id" class="die">
        <Die
          :number="die.face"
          :id="die.id"
          :left="Math.floor(Math.random() * 80)"
          :top="Math.floor(Math.random() * 90)"
          :rotate="Math.floor(Math.random() * 360)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Die from "@/components/DieComponent";

export default {
  components: {
    Die,
  },
  props: {
    dice: {
      type: Array,
      // default: () => [
      //   { id: 1, face: 1, holding: false },
      //   { id: 2, face: 6, holding: false },
      //   { id: 3, face: 4, holding: false },
      //   { id: 4, face: 5, holding: false },
      //   { id: 5, face: 5, holding: false },
      // ],
    },
  },
};
</script>

<style scoped>
.field {
  max-width: 399px;
  margin: auto;
  width: 100%;
  height: 300px;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.die {
  width: 15%;
  height: 125px;
  margin: 20px;
  position: relative;
}
</style>
