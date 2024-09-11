<template>
  <div class="main-content">
    <h1>Poke Memmories</h1>
    <h3>Select mode to start game</h3>
    <div class="buton-content">
      <div class="button-item">
        <button @click="onStart(16)">
          <span>4x4</span>
          <label for="">Easy</label>
        </button>
      </div>
      <div class="button-item">
        <button @click="onStart(36)">
          <span>6x6</span>
          <label for="">Nomarl</label>
        </button>
      </div>
      <div class="button-item">
        <button @click="onStart(64)">
          <span>8x8</span>
          <label for="">Hard</label>
        </button>
      </div>
      <div class="button-item">
        <button @click="onStart(100)">
          <span>10x10</span>
          <label for="">Super Hard</label>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(toTalBlocks) {
      this.$emit("onStart", toTalBlocks);
    },
  },
};
</script>

<style scoped>
.main-content {
  text-align: center;
}

.main-content h1 {
  font-size: 72px;
  color: #fff;
  text-transform: uppercase;
  font-weight: 700;
  margin-bottom: 15px;
}

.main-content h3 {
  font-size: 30px;
  color: #ffffff;
  margin-bottom: 40px;
}

.main-content .buton-content {
  display: flex;
  align-items: center;
  gap: 30px;
}

.main-content .buton-content .button-item button {
  width: 150px;
  height: 150px;
  border: 1px solid var(--light);
  border-radius: 15px;
  background: transparent;
  font-family: var(--font);
  cursor: pointer;
}

.main-content .buton-content .button-item button span {
  display: block;
  margin-bottom: 5px;
  font-size: 36px;
  color: var(--light);
}

.main-content .buton-content .button-item button label {
  font-size: 20px;
  color: var(--light);
}
</style>
