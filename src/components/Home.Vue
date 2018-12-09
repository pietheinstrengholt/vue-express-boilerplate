<template>
  <div class="container">
    <h1>The home component</h1>
    <div v-if="posts">
      <table border="1" class="table table-striped table-bordered">
        <thead>
          <tr class="success">
            <th>Name</th>
            <th>Description</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts">
            <td>{{ post.title }}</td>
            <td>{{ post.content }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: []
    };
  },
  created: function() {
    this.fetchData();
  },
  methods: {
    fetchData: function() {
      this.$http
        .get("http://localhost:3000/feed/posts")
        .then(response => {
          return response.json();
        })
        .then(data => {
          this.posts = data["posts"];
        });
    }
  }
};
</script>