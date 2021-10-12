<template>
  <div class="rating star-icon color-default" :class="cssClass">
    <div class="star-container">
      <div class="star" v-for="k in [0, 1, 2, 3, 4]" :key="k">
        <i class="star-empty"></i>
        <i class="star-half"></i>
        <i class="star-filled"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RatingStars',
  props: {
    rating: String,
  },
  computed: {
    cssClass() {
      return 'value-' + Math.round(this.rating).toString()
    },
  },
}
</script>
