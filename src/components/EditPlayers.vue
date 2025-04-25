<template>
  <h2 class="title">Редактирование игроков</h2>

  <div class="row">
    <EditPlayersItem
      v-for="player in playersList"
      :key="player.id"
      :player="player"
      @updateName="updateName"
      @updateLife="updateLife"
    />
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
import { EditPlayersItem } from ".";

const props = defineProps({
  playersList: {
    type: Array,
  },
});

const emit = defineEmits(["update-player"]);

const updateName = (id, newName) => {
  const player = props.playersList.find((p) => p.id === id);
  if (player) {
    emit("update-player", { ...player, name: newName });
  }
};

const updateLife = (id, delta) => {
  const player = props.playersList.find((p) => p.id === id);
  if (player) {
    const newLife = player.life + delta;
    emit("update-player", { ...player, life: newLife });
  }
};
</script>

<style lang="scss" scoped>
.title {
  margin-bottom: 24px;
}
.row {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
}
</style>