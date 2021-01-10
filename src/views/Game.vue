<template>
  <div class="game">
    <div>
      <h1 class="top-title">Turn 1: Player 1</h1>
    </div>
    <div class="field">
      <DiceField :dice="dice" />
    </div>
    <div class="controls">
      <button @click.prevent="send" class="roll-button">Roll Dice</button>

      <div class="scoreboard">
        <div class="title-scoreboard">Scoreboard</div>
        <ScoreTable/>
      </div>
    </div>
  </div>
</template>

<script>
import SockJS from "sockjs-client";
import Stomp from "webstomp-client";
import DiceField from "@/components/DiceField";

import ScoreTable from "@/components/ScoreTable";

export default {
  components: {
    DiceField,
    ScoreTable
  },
  name: "game",
  data() {
    return {
      dice: [
        { id: 1, face: 1, holding: false },
        { id: 2, face: 2, holding: false },
        { id: 3, face: 3, holding: false },
        { id: 4, face: 4, holding: false },
        { id: 5, face: 5, holding: false },
      ],

      connected: false,
    };
  },
  created() {
    this.connect();
  },
  methods: {
    send() {
      if (this.stompClient && this.stompClient.connected) {
        const msg = this.dice;
        console.warn(JSON.stringify(msg));
        this.stompClient.send("/app/roll", JSON.stringify(msg), {});
      }
    },
    connect() {
      this.socket = new SockJS("http://localhost:8096/gs-guide-websocket");
      this.stompClient = Stomp.over(this.socket);
      this.stompClient.connect(
        {},
        (frame) => {
          this.connected = true;
          console.log(frame);
          this.stompClient.subscribe("/game/dice", (tick) => {
            console.log(tick);
            //this.received_messages.push(JSON.parse(tick.body).content)
            this.setMessageOutput(JSON.parse(tick.body));
            console.warn(this.received_messages);
          });
        },
        (error) => {
          console.log(error);
          this.connected = false;
        }
      );
    },
    setMessageOutput(messageOutput) {
      console.warn(messageOutput);
      this.dice = messageOutput;
    },
    disconnect() {
      if (this.stompClient) {
        this.stompClient.disconnect();
      }
      this.connected = false;
    },
    tickleConnection() {
      this.connected ? this.disconnect() : this.connect();
    },
  },
};
</script>

<style scoped>
.title-scoreboard{
  text-align: center !important;
  margin-top: 0px;
  font-family: "Rubik One", Helvetica, Arial;
  text-align: left;
  font-size: 21px;
}
.scoreboard {
  width: 100%;
  
  background-color: #e3daca;
  padding: 1em 1em 1em 1em;
  border-radius: 16px;
  box-shadow: inset 0px 0px 32px #807c74;
}
.controls {
  display: flex;
  justify-content: center;
  flex-direction: column;
}
.roll-button {
  background-color: rgba(1, 1, 1, 0);
  color: #a69360;
  box-shadow: none;
  border: none;
  width: auto;
  font-size: 32px;
  display: inline-block;
  margin-top: 50px;
  font-weight: 600;
  margin-bottom: 50px;
}
.field {
  margin-bottom: 75px;
}
.top-title {
  font-weight: 600;
  font-size: 21px;
}
.game {
  text-align: left;
  font-family: "Montserrat Alternates", Helvetica, Arial;
}
</style>
