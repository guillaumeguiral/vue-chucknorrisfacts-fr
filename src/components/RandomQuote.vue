<template>
  <div class="quote-container">
    <div v-if="quote" class="quote">{{ quote.text }}</div>
    <RatingStars v-if="quote" class="score" :rating="quote.note"></RatingStars>
    <div
      class="quote-progress"
      :class="{ animated: quote }"
      v-on:animationend="nextQuote"
    ></div>
  </div>
</template>

<script>
import axios from 'axios'

import RatingStars from './RatingStars'

export default {
  name: 'RandomQuote',
  components: {
    RatingStars,
  },
  data() {
    return {
      quotes: [],
      quote: null,
    }
  },
  methods: {
    fetchAllQuotes() {
      axios
        .get('./data.json')
        .then((res) => {
          this.quotes = res.data
          this.getRandomQuote()
        })
        .catch((err) => console.log(err))
    },
    getRandomQuote() {
      this.quote = this.quotes[Math.floor(Math.random() * this.quotes.length)]
    },
    nextQuote() {
      this.quote = null
      setTimeout(() => this.getRandomQuote(), 1000)
    },
  },
  mounted() {
    this.fetchAllQuotes()
  },
}
</script>

<style lang="scss" scoped>
.quote-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;

  .quote {
    position: absolute;
    width: 70%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 3.2em;
    text-align: center;
    animation: fade-in 1s linear, fade-out 0.5s linear 11s forwards;
  }

  .score {
    position: absolute;
    bottom: 32px;
    left: 50%;
    transform: translate(-50%, 0);
    font-size: 0.8em;
    text-align: center;
    animation: fade-in 1s linear, fade-out 0.5s linear 11s forwards;
  }

  .quote-progress {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 4px;
    background-color: #666;

    &.animated {
      animation: progress 11.5s linear;
    }
  }
}

@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes fade-out {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

@keyframes progress {
  0% {
    width: 0%;
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  95% {
    opacity: 1;
  }
  100% {
    width: 100%;
    opacity: 0;
  }
}
</style>
