<template>
  <div id="app">
    <AppHeader
      :total="properties.length"
      :active="filteredProperties.length"
      v-model:search="searchQuery"
      :sort-order="sortOrder"
      @toggle-sort="toggleSort"
    />

    <main class="grid">
      <PropertyCard
        v-for="property in filteredProperties"
        :key="property.id"
        v-bind="property"
        :bookmarked="bookmarks.includes(property.id)"
        @toggle-bookmark="toggleBookmark"
      />
      <p v-if="filteredProperties.length === 0" class="empty-state">
        No properties found for "{{ searchQuery }}"
      </p>
    </main>
  </div>
</template>

<script>
import { properties } from './data/Properties.js'
import PropertyCard from './components/PropertyCard.vue'
import AppHeader from './components/AppHeader.vue'

export default {
  name: 'App',
  components: { PropertyCard, AppHeader },
  data() {
    return {
      properties,
      searchQuery: '',
      sortOrder: 'asc',        // 'asc' or 'desc'
      bookmarks: JSON.parse(localStorage.getItem('bookmarks') || '[]')
    }
  },
  computed: {
    filteredProperties() {
      const q = this.searchQuery.toLowerCase()
      return [...this.properties]
        .filter(p =>
          p.title.toLowerCase().includes(q) ||
          p.location.toLowerCase().includes(q)
        )
        .sort((a, b) =>
          this.sortOrder === 'asc' ? a.price - b.price : b.price - a.price
        )
    }
  },
  methods: {
    toggleSort() {
      this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc'
    },
    toggleBookmark(id) {
      if (this.bookmarks.includes(id)) {
        this.bookmarks = this.bookmarks.filter(b => b !== id)
      } else {
        this.bookmarks.push(id)
      }
      localStorage.setItem('bookmarks', JSON.stringify(this.bookmarks))
    }
  }
}
</script>