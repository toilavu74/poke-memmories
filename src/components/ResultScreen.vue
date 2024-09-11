<template>
  <div class="main-content">
    <h1>Congratulations</h1>
    <p>
      <span>{{ Math.round(timer / 1000) }}</span> senconds
    </p>
    <button @click="onStartGame()">Start Again</button>
  </div>
</template>
<script>
export default {
  methods: {
    onStartGame() {
      this.$emit("onAgain");
    },
  },
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
};
</script>
<style scoped>
.main-content h1 {
  color: var(--light);
  font-size: 60px;
  margin-bottom: 20px;
  text-transform: uppercase;
  text-align: center;
  font-weight: bold;
}
.main-content p {
  color: var(--light);
  font-size: 30px;
  margin-bottom: 30px;
  text-align: center;
}
.main-content p span {
  color: var(--primary);
}
.main-content button {
  margin: 0 auto;
  display: block;
  width: 150px;
  height: 50px;
  line-height: 50px;
  border: 0px;
  font-size: 16px;
  border-radius: 7px;
  text-transform: uppercase;
  color: var(--dark);
  background-color: var(--primary);
  font-family: var(--font);
  font-weight: bold;
  cursor: pointer;
}
</style>
