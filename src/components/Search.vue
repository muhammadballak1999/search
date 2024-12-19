<template>
  <div class="container">
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search articles..."
      class="search-bar"
    />

    <p v-if="filteredArticles.length !== 0" class="count-message">
      {{ filteredArticles.length }} {{ filteredArticles.length === 1 ? 'post' : 'posts' }} found
    </p>
    <p v-else class="count-message">
      No posts found
    </p>

    <div v-for="article in filteredArticles" :key="article.id" class="article">
      <h2 v-html="highlightText(article.title)"></h2>
      <p><strong>{{ article.date }}</strong></p>
      <p v-html="highlightText(article.content)"></p>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const searchQuery = ref("");
    const articles = ref([
      { id: 1, title: "Vue", date: "2024-12-10", content: "Getting started with Vue.js" },
      { id: 2, title: "Lorem", date: "2024-12-15", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 3, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 4, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 5, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 6, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 7, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 8, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 9, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 10, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 11, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 12, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 13, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 14, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 15, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 16, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 17, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 18, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 19, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },
      { id: 20, title: "Lorem", date: "2024-12-01", content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit." },

    ]);

    const filteredArticles = computed(() => {
      return articles.value.filter((article) => {
        const query = searchQuery.value.toLowerCase();
        return (
          article.title.toLowerCase().includes(query) ||
          article.content.toLowerCase().includes(query) ||
          article.date.includes(query)
        );
      });
    });

    const highlightText = (text) => {
      if (!searchQuery.value) return text;
      const query = searchQuery.value.toLowerCase();
      const regex = new RegExp(`(${query})`, "gi");
      return text.replace(regex, '<span class="highlight">$1</span>');
    };

    return {
      searchQuery,
      filteredArticles,
      highlightText
    };
  }
};
</script>

<style>
.container {
  width: 100%;
  height: 100%;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.search-bar {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border: 2px solid #ddd;
  border-radius: 8px;
  box-sizing: border-box;
  margin-bottom: 20px;
  transition: border-color 0.3s ease-in-out;
}

.search-bar:focus {
  outline: none;
  border-color: #007bff;
}

.count-message {
  font-size: 14px;
  font-weight: 600;
  color: #555;
  margin-bottom: 20px;
}

.count-message p {
  margin: 0;
}

.article {
  padding: 20px;
  margin-bottom: 20px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s ease-in-out;
}

.article:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.article h2 {
  font-size: 24px;
  font-weight: 600;
  margin: 0;
  color: #333;
  line-height: 1.4;
}

.article p {
  font-size: 16px;
  color: #666;
  line-height: 1.6;
}

.article .date {
  font-size: 14px;
  color: #999;
  margin-top: 10px;
}

.highlight {
  background-color: #ffeb3b;
  padding: 0 2px;
  font-weight: 600;
  border-radius: 3px;
}

@media (max-width: 768px) {
  .container {
    padding: 15px;
  }

  .search-bar {
    padding: 10px;
    font-size: 14px;
  }

  .article {
    padding: 15px;
  }

  .article h2 {
    font-size: 20px;
  }

  .article p {
    font-size: 14px;
  }
}
</style>