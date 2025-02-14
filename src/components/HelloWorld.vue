<template>
  <audio 
    src="@/assets/yung-kai-blue-(official-audio)-made-with-Voicemod.mp3"
    ref="backgroundAudio"
    loop
  ></audio>

  <div class="container" v-if="!showImage">
    <h1>Will You Be My Valentine?</h1>
    <p>{{ curentMessage }}</p>
    <img v-if="noButtonClickedCnt > 0" :src="currentRejectionGif" alt="rejected-milk-and-mocha">
    <div class="options-container">
      <button class="yes-button" @click="showGifAndHearts">YES</button>
      <!-- Use ref to access the button directly -->
      <button 
        class="no-button" 
        v-if="!noButtonClicked" 
        @click="getMessage"
        ref="noButton"
      >
        NO
      </button>
    </div>
  </div>

  <!-- Conditional If The User Clicks On The YES Button -->
  <GifDisplay v-if="showImage" :gifSrc="require('@/assets/milk-and-mocha.gif')" />
  <FallingEffects v-if="showHearts" emoji-type="happy"/>
</template>

<script>
import FallingEffects from './FallingEffects.vue';
import GifDisplay from './GifDisplay.vue';

export default {
  name: 'HelloWorld',
  components: {
    GifDisplay,
    FallingEffects
  },
  data() {
    return {
      showImage: false,
      showHearts: false,
      noButtonClicked: false,
      noButtonClickedCnt: 0,
      rejectionSentences: [
        "I Think You Missclicked The Yes Button",
        "You're Kidding Right?",
        "You're Not Being Fr... Right?",
        "Are You Srs Right Neow Pookie Bear?",
        "I Guess There's Only One Option"
      ],
      curentMessage: "",
      rejectionGif: [
        require("@/assets/milk-and-mocha (2).webp"),
        require("@/assets/milk-and-mocha (1).webp"),
        require("@/assets/milk-and-mocha.webp"),
        require("@/assets/milk-and-mocha-sad.webp"),
        require("@/assets/milk-and-mocha (3).webp"),
      ],
      currentRejectionGif: "",
    };
  },
  methods: {
    moveButton() {
      // Check if the button exists before trying to access its style
      const noButton = this.$refs.noButton;

      if (noButton) {
        // Get random values for top and left
        const randTop = Math.floor(Math.random() * (window.innerHeight - 100));
        const randLeft = Math.floor(Math.random() * (window.innerWidth - 100));

        setTimeout(() => {
          // Move the button to a random position
          noButton.style.position = "absolute";
          noButton.style.top = `${randTop}px`;
          noButton.style.left = `${randLeft}px`;
        }, 10);
      }
    },

    getMessage() {
      this.noButtonClickedCnt++;

      if (this.noButtonClickedCnt >= 5) {
        this.noButtonClicked = true;
      }

      this.currentRejectionGif = this.rejectionGif[this.noButtonClickedCnt - 1];
      console.log("Current Rejection GIF Path:", this.currentRejectionGif)

      this.curentMessage = this.rejectionSentences[this.noButtonClickedCnt - 1];

      this.moveButton();
    },

    // Method to show the GIF when YES button is clicked
    showGifAndHearts() {
      this.showImage = true;
      this.showHearts = true;

      const audio = this.$refs.backgroundAudio;
      audio.src = require("@/assets/yung-kai-blue-(official-audio)-made-with-Voicemod.mp3");
      audio.play().catch(error => {
        console.log("Error In Playing Audio", error);
      });
    }
  }
};
</script>

<style>
.container {
  background-color: white;
  margin: 1em;
  border-radius: 1em;
  padding: 3em;
}

.options-container {
  display: flex;
  justify-content: space-around;
}

button {
  color: white;
  padding: 1em 2em;
  border: none;
  cursor: pointer;
  border-radius: 30px;
  transition: all 0.3s ease-in-out;
  display: flex;
  align-items: center;
  justify-content: center;
}

.yes-button {
  background-color: #ff69b4; /* Pink color */
  position: relative;
}

.yes-button:hover {
  background-color: #ff1493; /* Darker pink on hover */
  transform: scale(1.1); /* Slightly enlarge on hover */
}

.no-button {
  background-color: #A1A1A1; /* Tomato red color */
  position: relative;
}

.no-button:hover {
  background-color: black;
}

.no-message {
  color: #C177B2; /* Customize the text color for the message */
  margin-top: 20px;
  font-size: 1.2em;
  font-weight: bold;
}
</style>
