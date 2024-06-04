<template>
  <div class="container">
    <form @submit.prevent="save" class="form">
      <input type="text" v-model="form.title" placeholder="Title" /><br />
      <textarea v-model="form.content" placeholder="Content"></textarea><br />
      <button type="submit">Save</button>
    </form>

    <ul class="article-list">
      <li v-for="article in articles" :key="article.id" class="article-item">
        <h3>{{ article.title }}</h3>
        <p>{{ article.content }}</p>
        <button @click="edit(article)">Edit</button>
      </li>
    </ul>

    <button @click="load" class="load-button">Load</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        title: '',
        content: ''
      },
      articles: []
    };
  },
  methods: {
    save() {
      if (this.form.title && this.form.content) {
        this.articles.push({
          id: this.articles.length + 1,
          title: this.form.title,
          content: this.form.content
        });
        this.form.title = '';
        this.form.content = '';
      }
    },
    edit(article) {
      this.form.title = article.title;
      this.form.content = article.content;
      this.articles = this.articles.filter(a => a.id !== article.id);
    },
    load() {
      // Contoh data yang di-load, ganti dengan logika load sebenarnya
      this.articles = [
        { id: 1, title: 'judul', content: 'Ini Content' },
        { id: 2, title: 'judul 2', content: 'Ini Content 2' },
        { id: 3, title: 'judul 3', content: 'Ini Content 3' }
      ];
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.form input[type="text"],
.form textarea {
  width: 100%;
  margin-bottom: 10px;
  padding: 5px;
  font-size: 16px;
}

.form button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

.form button:hover {
  background-color: #45a049;
}

.article-list {
  list-style-type: none;
  padding: 0;
}

.article-item {
  margin-bottom: 20px;
  padding: 10px;
  background-color: #000000;
}

.article-item h3 {
  margin-top: 0;
}

.article-item button {
  background-color: #ff5722;
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
}

.article-item button:hover {
  background-color: #f44336;
}
</style>
