<template>
  <div class="player">
    <input
      class="input"
      :value="player.name"
      @input="updateName(player.id, $event.target.value)"
    />
    <button class="button" @click="updateLife(player.id, -1)">-</button>
    <span class="life-count">{{ player.life }}</span>
    <button class="button" @click="updateLife(player.id, 1)">+</button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

defineProps({
  player: {
    type: Object,
  },
});

const emit = defineEmits(["updateName", "updateLife"]);

const updateName = (id, newName) => {
  emit("updateName", id, newName);
};

const updateLife = (id, delta) => {
  emit("updateLife", id, delta);
};
</script>

<style lang="scss" scoped>
.player {
  display: flex;
  align-items: center;
  width: 100%;

  .input {
    margin-right: 12px;
  }

  .button {
    max-width: 30px;
  }

  .life-count {
    min-width: 30px;
    text-align: center;
  }
}
</style>
