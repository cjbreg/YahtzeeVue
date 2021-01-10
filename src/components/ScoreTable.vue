<template>
  <div>
    <table class="table">
      <tr>
        <th class="top-left">Part 1</th>
        <th>Player 1</th>
        <th>Player 2</th>
      </tr>
      <tr v-for="score in scoresPart1" :key="score.id">
        <td>{{ score.type }}</td>
        <td>{{ points }}</td>

        <td>{{ points }}</td>
      </tr>
      <tr>
        <td>Total Part 1</td>
        <td></td>
        <td></td>
      </tr>
    </table>

    <table class="table">
      <tr>
        <th class="top-left">Part 2</th>
        <th>Player 1</th>
        <th>Player 2</th>
      </tr>
      <tr v-for="score in scoresPart2" :key="score.id">
        <td>{{ score.type }}</td>
        <td>{{ points }}</td>
        <td>{{ points }}</td>
      </tr>
      <tr>
        <td>Total Part 2</td>
        <td></td>
        <td></td>
      </tr>
      <tr>
        <td class="total-score">Total score</td>
        <td></td>
        <td></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      scoresPart1: [
        { id: 1, type: "Three of a Kind", points: null },
        { id: 2, type: "Four of a Kind", points: null },
        { id: 3, type: "Full House", points: null },
        { id: 4, type: "Small Straight", points: null },
        { id: 5, type: "Large Straight", points: null },
        { id: 6, type: "Yahtzee", points: null },
        { id: 7, type: "Chance", points: null },
      ],
      scoresPart2: [
        { id: 1, type: "Aces", points: null },
        { id: 2, type: "Twos", points: null },
        { id: 3, type: "Threes", points: null },
        { id: 4, type: "Fours", points: null },
        { id: 5, type: "Fives", points: null },
        { id: 6, type: "Sixes", points: null },
      ],
    };
  },
};
</script>

<style scoped>
.top-left {
  background-color: #907604;
  color: #e3daca;
  font-size: 17px;
}

.total-score {
  background-color: #907604;
  color: #e3daca;
  font-size: 13px;
}
table {
  border-collapse: collapse;
}
td,
th {
  border: 1px solid #907604;
  text-align: left;
  font-size: 13px;
  padding: 2px;
}
th {
  text-align: center;
}
</style>
