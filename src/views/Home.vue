<template>
  <div class="home">
    <h1 class="title">Yahtzee</h1>
    <div class="center-images">
      <img src="../assets/Dice/die-1-white.svg" alt="" class="die-image" />
      <img src="../assets/Dice/die-2-dark.svg" alt="" class="die-image" />
      <img src="../assets/Dice/die-3-white.svg" alt="" class="die-image" />
      <img src="../assets/Dice/die-4-dark.svg" alt="" class="die-image" />
      <img src="../assets/Dice/die-5-white.svg" alt="" class="die-image" />
      <img src="../assets/Dice/die-6-dark.svg" alt="" class="die-image" />
    </div>
    <button @click.prevent="connect" class="ready-button">Ready</button>
    <H3>{{ userlegit }}</H3>
    <H3>{{ error_message }}</H3>
  </div>
</template>
<script>
import SockJS from "sockjs-client";
import Stomp from "webstomp-client";

export default {
  name: "home",
  data() {
    return {
      userlegit: null,
      error_message: null,
      send_message: null,

      send_name: null,
      connected: false,
    };
  },
  methods: {
    send() {
      if (this.stompClient && this.stompClient.connected) {
        var user = JSON.parse(window.localStorage.getItem("user"));
        if (user == null) {
          this.userlegit = false;
        } else {
          const msg = {
            id: user.id,
            username: user.username,
            accessToken: user.accessToken,
          };
          console.log(JSON.stringify(msg));
          this.stompClient.send("/app/auth", JSON.stringify(msg), {});
        }
      }
    },
    connect() {
      this.socket = new SockJS("http://localhost:8096/gs-guide-websocket");
      this.stompClient = Stomp.over(this.socket);
      this.stompClient.connect(
        {},
        (frame) => {
          this.connected = true;
          if (this.connected == true) {
            console.warn("connected bb");
            this.send();
          }
          console.log(frame);
          this.stompClient.subscribe("/auth/user", (tick) => {
            console.log(tick);
            //this.received_messages.push(JSON.parse(tick.body).content)
            this.setMessageOutput(JSON.parse(tick.body));
            //console.warn(this.received_messages);
          });
        },
        (error) => {
          console.log(error);
          this.connected = false;
        }
      );
    },
    setMessageOutput(messageOutput) {
      this.userlegit = messageOutput;
      this.startGame();
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
    startGame() {
      if (!this.userlegit) {
        this.error_message = "Something went wrong";
      } else {
        this.$router.push("/game");
      }
    },
  },
  mounted() {
    // this.connect();
  },
};
</script>
<style scoped>
.ready-button {
  background-color: rgba(1, 1, 1, 0);
  color: #a69360;
  box-shadow: none;
  border: none;
  text-decoration: underline;
  width: auto;
  font-family: "Rubik One", Arial, Helvetica, sans-serif;
  font-size: 32px;
  display: inline-block;
  margin-top: 50px;
}
.home {
  text-align: center;
  padding-top: 75px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.title {
  font-family: "Rubik One", Arial, Helvetica, sans-serif;
  margin-bottom: 50px;
}

.center-images {
  justify-content: space-between;
  display: flex;
  flex-wrap: wrap;
  width: 300px;
}
.die-image {
  height: 80px;
  width: 80px;
  margin: 10px;
}
</style>
