<template>
  <div class="falling-elements">
    <!-- Generate a large number of emojis with random styles -->
    <div 
      class="falling-item" 
      v-for="n in emojiCount" 
      :key="'emoji-' + n" 
      :style="getRandomStyle()"
    >
      <!-- Randomly choose between heart and flower emojis or sad emojis -->
      <span v-if="emojiType === 'happy'">
        <span v-if="Math.random() > 0.5">❤️</span>
        <span v-else>🌸</span>
      </span>
      <span v-else>
        <span v-if="Math.random() > 0.5">😢</span>
        <span v-else>💔</span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "FallingEffects",
  props: {
    emojiType: String, // Prop to determine if it's happy or sad
  },
  data() {
    return {
      emojiCount: 100, // Number of falling emojis
    };
  },
  methods: {
    // Generate random style for each emoji
    getRandomStyle() {
      const randLeft = Math.floor(Math.random() * 100) + "%"; 
      const randDelay = Math.random() * 5 + "s"; 
      const randDuration = Math.floor(Math.random() * (10 - 4 + 1) + 4) + "s"; 

      return {
        left: randLeft,
        animationDelay: randDelay,
        animationDuration: randDuration,
        animationTimingFunction: "cubic-bezier(0.25, 0.8, 0.25, 1)", 
      };
    },
  },
};
</script>

<style scoped>
.falling-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
}

.falling-item {
  position: absolute;
  font-size: 30px;
  opacity: 0.8;
  animation: fall linear infinite;
}

@keyframes fall {
  0% {
    transform: translateY(-100px);
    opacity: 1;
  }
  100% {
    transform: translateY(calc(100vh + 100px));
    opacity: 0;
  }
}
</style>
