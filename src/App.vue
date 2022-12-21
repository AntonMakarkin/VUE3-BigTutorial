<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <MyInput placeholder="Поиск..." v-model="searchQuery"/>
    <div class="app_btns">
      <MyButton @click="showDialog">Создать пост</MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions"/>
    </div>
    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost"/>
    </MyDialog>
    <PostList :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostLoading" />
    <div v-else>Идет загрузка...</div>
    <div class="page__wrapper">
      <div 
        v-for="page in totalPages" 
        :key="page"
        class="page"
        >
        {{ page }}
        </div>
    </div>
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
        posts: [],
        dialogVisible: false,
        isPostLoading: false,
        selectedSort: '',
        searchQuery: '',
        page: 1,
        limit: 10,
        totalPages: 1,
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По содержимому'}
        ]
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
          this.isPostLoading = true;
            const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
              params: {
                _page: this.page,
                _limit: this.limit
              }
            })
            this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
            this.posts = response.data;
        } catch (e) {
          alert('Ошибка')
        } finally {
          this.isPostLoading = false
        }
      }
    },
    mounted() {
      this.fetchPosts();
    },
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
      },
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      }
    },
    watch: {
      
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

  .app_btns {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
  }

  .page__wrapper {
    display: flex;
    margin-top: 15px;
  }

  .page {
    border: 1px solid black;
    padding: 10px;
  }

  .current-page {
    border: 2px solid teal;
  }
</style>
