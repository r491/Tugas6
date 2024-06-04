<template>
  <div>
    <header>
      <h1>Simple Article Editor</h1>
    </header>
    <main>
      <form @submit.prevent="save">
        <input type="text" v-model="form.title" placeholder="Title" /><br />
        <textarea v-model="form.content" placeholder="Content"></textarea><br />
        <button type="submit">Save</button>
      </form>

      <ul>
        <li v-for="article in articles" :key="article.id">
          <h2>{{ article.title }}</h2>
          <p>{{ article.content }}</p>
          <button @click="edit(article)">Edit</button>
        </li>
      </ul>

      <button @click="load">Load</button>
    </main>
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
      // Optional: remove the article from the list to simulate an edit
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
header {
  background-color: #333;
  color: #fff;
  padding: 20px;
  text-align: center;
}

h1 {
  margin: 0;
}

main {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

form input[type="text"],
form textarea {
  width: 100%;
  margin-bottom: 10px;
  padding: 5px;
  font-size: 16px;
}

form button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

form button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 20px;
  padding: 10px;
  background-color: #000000;
}

li h2 {
  margin-top: 0;
}

li button {
  background-color: #ff5722;
  color: white;
  padding: 5px 10px;
  border: none;
  cursor: pointer;
}

li button:hover {
  background-color: #f44336;
}
</style>
