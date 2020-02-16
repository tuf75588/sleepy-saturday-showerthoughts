<template>
  <div id="app">
    <full-page :options="options" id="fullpage" v-if="loaded">
      <div v-for="post in posts" :key="post.data.id" class="section">
        <div class="container">
          <img src="./assets/shower.png" alt="shower icon" />

          <div class="quote-symbol">“</div>
          <p class="quote">
            <a :href="post.data.url">{{ post.data.title }}</a>
          </p>
          <div class="details">
            <div class="details-author">Author: {{ post.data.author }}</div>
            <div
              class="details-stats"
            >{{ post.data.ups }} Upvotes | {{ post.data.num_comments }} Comments</div>
          </div>
        </div>
      </div>
    </full-page>
    <div v-else>
      <h1>Loading..</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  created() {
    return fetch(
      "https://www.reddit.com/r/showerthoughts/top.json?limit=20&t=all"
    )
      .then(response => {
        return response.json();
      })
      .then(({ data }) => {
        this.posts = data.children;
        this.loaded = true;
      });
  },
  data() {
    return {
      posts: [],
      loaded: false,
      options: {
        navigation: true,
        sectionsColor: [
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#ba5be9",
          "#b4b8ab",
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#1bcee6",
          "#ee1a59",
          "#ba5be9",
          "#b4b8ab",
          "#41b883",
          "#ff5f45",
          "#0798ec",
          "#fec401",
          "#fec401",
          "#fec401"
        ]
      }
    };
  }
};
</script>

<style>
#app {
  font-family: sans-serif;
  color: #2d3748;
}
body {
  margin: 0;
  padding: 0;
}
h3 {
  margin: 0;
}
.container {
  margin: auto;
  max-width: 800px;
  padding: 80px 16px;
}
.section {
  text-align: center;
}
.quote-symbol {
  font-size: 64px;
  line-height: 0;
  margin-top: 50px;
  color: white;
}
.quote a {
  text-decoration: none;
  font-family: "Sriracha", cursive;
  color: white;
  font-size: 36px;
  line-height: 1.5;
}
.quote a:hover {
  color: #edf2f7;
}

.details-stats {
  margin-top: 4px;
}
</style>
