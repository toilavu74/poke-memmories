<template>
  <div class="main-content" :class="classObject">
    <card-item
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="checkRule($event)"
    />
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";
export default {
  name: "InteractScreen",
  components: {
    CardItem,
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
    totalOfBlocks: {
      type: Number,
    },
  },
  data() {
    return {
      localTotalOfBlocks: this.totalOfBlocks,
      rules: [],
    };
  },
  computed: {
    classObject() {
      return {
        cards__16: this.localTotalOfBlocks == 16,
        cards__36: this.localTotalOfBlocks == 36,
        cards__64: this.localTotalOfBlocks == 64,
        cards__100: this.localTotalOfBlocks == 100,
      };
    },
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
        this.rules = [];
        const disabledElement = document.querySelectorAll(
          ".main-content .card.disabled"
        );
        if (
          disabledElement &&
          disabledElement.length == this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
<style scoped>
.main-content.cards__16 {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.main-content.cards__36 {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 10px;
}

.main-content.cards__64 {
  display: grid;
  grid-template-columns: repeat(16, 1fr);
  gap: 10px;
}

.main-content.cards__100 {
  display: grid;
  grid-template-columns: repeat(20, 1fr);
  gap: 10px;
}
</style>
