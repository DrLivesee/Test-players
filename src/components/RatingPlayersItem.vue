<template>
  <div class="player">
    <div
      class="rating-position"
      :class="{
        gold: index === 0,
        silver: index === 1,
        bronze: index === 2,
      }"
    >
      {{ index + 1 }}
    </div>
    <div class="rating-info">
      У игрока <b>{{ player.name }}</b> {{ player.life }} жизней
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

defineProps({
  index: {
    type: Number,
  },
  player: {
    player: Object,
  },
});
</script>

<style lang="scss" scoped>
.player {
  .rating-position {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background: white;
    color: black;
    font-weight: bold;

    &.gold {
      background: #ffd700;
    }

    &.silver {
      background: #c0c0c0;
    }

    &.bronze {
      background: #cd7f32;
    }
  }

  .rating-info {
    flex: 1;
    text-align: left;

    b {
      color: #2c3e50;
    }
  }
}
</style>
