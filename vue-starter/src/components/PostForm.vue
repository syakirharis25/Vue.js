<template>
  <form v-if="!loading" class="form" @submit.prevent="onSubmit">
      <div class="input-field">
          <label for="title">Title</label>
          <input type="text"
            name="title"
            v-model="title"
            class="validate"
          >
          <span class="helper-text" data-error="Title must not be empty"></span>
      </div>
      <div class="input-field">
          <label for="body">Body</label>
          <input type="text"
            name="body"
            v-model="body"
            class="validate"
          >
          <span class="helper-text" data-error="Body must not be empty"></span>
      </div>
      <button type="submit" class="waves-effect waves-light btn">
          Add
      </button>
  </form>
</template>

<script>
import PostService from './PostService';
const postService = new PostService();
export default {
    name: "PostForm",
    data(){
        return {
            loading: false,
            title: '',
            body: ''
        };
    },
    methods: {
        onSubmit(){
            this.loading = true;
            const post = {
                title: this.title,
                body: this.body
            };

            postService.writePost(post)
                .then(res => {
                    console.log(res.data);
                })
                .catch(err => console.error(err));
        }
    }
}
</script>

<style>
.form {
    margin: 50px;
}
</style>