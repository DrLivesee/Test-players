<template>
  <div>
    <h2 class="title">Рейтинг</h2>
    <div class="rating-container">
      <RatingPlayersItem
        v-for="(player, index) in ratingPlayers"
        :key="player.id"
        :player="player"
        :index="index"
        class="rating-item"
      />
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import { RatingPlayersItem } from ".";

defineProps({
  ratingPlayers: {
    type: Object,
  },
});
</script>

<style lang="scss" scoped>
.title {
  margin-bottom: 24px;
}

.rating-container {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.rating-item {
  display: flex;
  align-items: center;
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 6px;
  background: #f8f8f8;
  gap: 15px;

  &:nth-child(even) {
    background: #f0f0f0;
  }
}
</style>
