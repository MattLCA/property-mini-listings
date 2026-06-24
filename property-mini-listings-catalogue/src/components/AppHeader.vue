<template>
  <header class="app-header">
    <div class="header-top">
      <div>
        <h1 class="brand">PropFinder</h1>
        <p class="count">{{ active }} of {{ total }} listings</p>
      </div>
      <button class="sort-btn" @click="$emit('toggle-sort')">
        {{ sortOrder === 'asc' ? '↑ Price: Low to High' : '↓ Price: High to Low' }}
      </button>
    </div>
    <input
      class="search-input"
      type="text"
      placeholder="Search by title or location…"
      :value="search"
      @input="$emit('update:search', $event.target.value)"
    />
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    total:     { type: Number, required: true },
    active:    { type: Number, required: true },
    search:    { type: String, default: '' },
    sortOrder: { type: String, default: 'asc' }
  },
  emits: ['update:search', 'toggle-sort']
}
</script>