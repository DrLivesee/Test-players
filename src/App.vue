<template>
  <div class="content">
    <div class="tabs">
      <button
        class="tab-button"
        :class="{ active: activeTab === 'create' }"
        @click="activeTab = 'create'"
      >
        Создание игрока
      </button>
      <button
        class="tab-button"
        :class="{ active: activeTab === 'edit' }"
        @click="activeTab = 'edit'"
        :disabled="!playersList.length"
      >
        Редактирование игроков
      </button>
    </div>

    <div class="tab-content">
      <template v-if="activeTab === 'create'">
        <CreatePlayer @create-player="createPlayer" />
      </template>
      <template v-else-if="activeTab === 'edit'">
        <EditPlayers :playersList="playersList" @update-player="updatePlayer" />
      </template>
    </div>

    <RatingPlayers v-if="ratingPlayers.length" :ratingPlayers="ratingPlayers" />
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import { EditPlayers, CreatePlayer, RatingPlayers } from "./components";

const activeTab = ref("create");
const playersList = ref([]);

const createPlayer = (player) => {
  playersList.value.push(player);
};

const updatePlayer = (updatedPlayer) => {
  const index = playersList.value.findIndex((p) => p.id === updatedPlayer.id);
  if (index !== -1) {
    playersList.value[index] = updatedPlayer;
  }
};

const ratingPlayers = computed(() =>
  [...playersList.value].sort((a, b) => b.life - a.life)
);
</script>

<style lang="scss">
@import "./assets/main.scss";

.content {
  display: flex;
  flex-direction: column;
  gap: 32px;

  .tabs {
    display: flex;
    gap: 8px;
    border-bottom: 1px solid #ddd;
    padding-bottom: 8px;

    .tab-button {
      padding: 8px 16px;
      background: none;
      border: none;
      border-radius: 4px 4px 0 0;
      cursor: pointer;
      font-size: 16px;
      transition: all 0.2s;

      &:hover {
        background: #f0f0f0;
      }

      &.active {
        background: #2c3e50;
        color: white;
        font-weight: bold;
      }

      &:disabled {
        opacity: 0.5;
        cursor: not-allowed;
      }
    }
  }

  .tab-content {
    border: 1px solid #eee;
    border-radius: 0 8px 8px 8px;
    padding: 16px;
  }
}
</style>
