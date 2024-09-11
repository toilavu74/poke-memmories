<template>
  <div class="poke-app">
    <main-screen
      v-if="startMatch === 'default'"
      @onStart="onHandleBeforeStart($event)"
    />
    <interact-screen
      v-if="startMatch === 'match'"
      :cardsContext="settings.cardsContext"
      :totalOfBlocks="settings.totalOfBlocks"
      @onFinish="onGetResult()"
    />
    <result-screen
      v-if="startMatch === 'result'"
      :timer="timer"
      @onAgain="onAgainGame()"
    />
    <copy-right />
  </div>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import CopyRight from "./components/CopyRight.vue";
import { shuffled } from "./utils/array";
import ResultScreen from "./components/ResultScreen.vue";
export default {
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      startMatch: "default",
      timer: 0,
    };
  },
  methods: {
    onHandleBeforeStart(configs) {
      //console.log("running..", configs);
      this.settings.totalOfBlocks = configs;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      //console.log(cards);
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      //console.log(this.settings.cardsContext);
      this.settings.startedAt = new Date().getTime();
      this.startMatch = "match";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.startMatch = "result";
    },
    onAgainGame() {
      this.startMatch = "default";
    },
  },
  components: {
    MainScreen,
    InteractScreen,
    CopyRight,
    ResultScreen,
  },
  name: "App",
};
</script>
<style>
.poke-app {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #333;
}
.poke-app .copyright {
  position: fixed;
  width: 100%;
  left: 0;
  right: 0;
  margin: 0 auto;
  bottom: 40px;
  text-align: center;
}
.poke-app .copyright p {
  font-size: 20px;
  color: var(--light);
  letter-spacing: 1px;
}
.poke-app .copyright p span {
  color: var(--primary);
}
</style>
