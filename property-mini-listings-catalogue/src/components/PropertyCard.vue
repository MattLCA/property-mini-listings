<template>
  <div class="card" :class="{ unavailable: !available }">
    <!-- Not Available ribbon -->
    <div v-if="!available" class="ribbon">Not Available</div>

    <!-- Bookmark button -->
    <button class="bookmark-btn" @click="$emit('toggle-bookmark', id)" :aria-label="bookmarked ? 'Remove bookmark' : 'Bookmark'">
      {{ bookmarked ? '♥' : '♡' }}
    </button>

    <img :src="image" :alt="title" class="card-image" />

    <div class="card-body">
      <span class="type-badge">{{ type }}</span>
      <h2 class="card-title">{{ title }}</h2>
      <p class="card-location">📍 {{ location }}</p>
      <p class="card-price">R {{ price.toLocaleString() }} / month</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyCard',
  props: {
    id:         { type: Number, required: true },
    title:      { type: String, required: true },
    location:   { type: String, required: true },
    price:      { type: Number, required: true },
    type:       { type: String, required: true },
    available:  { type: Boolean, default: true },
    image:      { type: String, required: true },
    bookmarked: { type: Boolean, default: false }
  },
  emits: ['toggle-bookmark']
}
</script>