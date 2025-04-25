<template>
  <h2 class="title">Добавить нового игрока</h2>
  <div class="row">
    <input
      class="input name"
      type="text"
      v-model="playersName"
      placeholder="Имя"
    />
    <input
      class="input life"
      type="number"
      v-model="playersLife"
      placeholder="Жизней"
    />
    <button class="button" type="button" @click="createPlayer">Создать</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const playersName = ref("");
const playersLife = ref(null);

const emit = defineEmits(["create-player"]);

const checkParameters = () => {
  if (!playersName.value) {
    alert("Укажите имя");
    return false;
  }

  if (!playersLife.value) {
    alert("Укажите количество жизней");
    return false;
  }

  if (playersLife.value <= 0) {
    alert("Значение не может быть меньше либо равно нулю");
    return false;
  }

  return true;
};

const clearPlayer = () => {
  playersName.value = "";
  playersLife.value = null;
};

const generateRandomId = () => {
  return Math.floor(1000000000 + Math.random() * 9000000000);
}

const createPlayer = () => {
  if (!checkParameters()) return;

  const newPlayer = { name: playersName.value, life: playersLife.value, id: generateRandomId()};

  emit("create-player", newPlayer);

  clearPlayer();
};
</script>

<style lang="scss" scoped>
.title {
  margin-bottom: 24px;
}
.row {
  display: flex;
  align-items: center;

  .input {
    margin-right: 12px;
  }
  .life {
    max-width: 120px;
  }

  .button {
    max-width: 90px;
  }
}
</style>
