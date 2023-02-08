<template>
  <div class="container">
    <BookCard v-for="book of books" :key="book.id" :item="book" />
  </div>
</template>

<script>
import BookCard from "@/components/BookCard.vue";
export default {
  components: {
    BookCard,
  },
  data() {
    return {
      books: [],
    };
  },
  methods: {
    async loadBooks() {
      const res = await fetch("http://localhost:4730/books");
      return await res.json();
    },
    loadFavorites() {
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];

      for (let i = 0; i < this.books.length; i++) {
        this.books[i].favorite = favorites.includes(this.books[i].isbn);
      }
    },
  },
  async created() {
    this.books = await this.loadBooks();
    this.loadFavorites();
  },
};
</script>
