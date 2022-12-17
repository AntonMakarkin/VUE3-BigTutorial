<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <MyButton @click="fetchPosts">Получить посты</MyButton>
    <MyButton @click="showDialog" style="margin: 15px 0">Создать пост</MyButton>
    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost"/>
    </MyDialog>
    <PostList :posts="posts" @remove="removePost"/>
  </div>
</template>

<script>
  import PostForm from "@/components/PostForm.vue";
  import PostList from "@/components/PostList.vue";
  import axios from 'axios';

  export default {
    components: {
      PostForm,
      PostList
    },
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript', body: 'Описание поста'},
          {id: 2, title: 'JavaScript', body: 'Описание поста 2'},
          {id: 3, title: 'JavaScript', body: 'Описание поста 3'},
        ],
        dialogVisible: false,
        modificatorValue: ''
      }
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialogVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },
      showDialog() {
        this.dialogVisible = true;
      },
      async fetchPosts() {
        try {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          console.log(response)
        } catch (e) {
          alert('Ошибка')
        }
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .app {
    padding: 20px;
  }
</style>
