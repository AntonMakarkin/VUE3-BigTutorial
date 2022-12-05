<template>
  <div class="app">
    <form>
      <input class="input" type="text" placeholder="Название">
      <input class="input" type="text" placeholder="Описание">
      <button class="btn">Создать</button>
    </form>
    <div class="post" v-for="post in posts" key:="post.id">
      <div><strong>Название:</strong>{{ post.title }}</div>
      <div><strong>Описание:</strong>{{ post.body }}</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript', body: 'Описание поста'},
          {id: 2, title: 'JavaScript', body: 'Описание поста 2'},
          {id: 3, title: 'JavaScript', body: 'Описание поста 3'},
        ]
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

  .post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
  }

  .form {
    display: flex;
    flex-direction: column;
  }

  .input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
  }

  .btn {
    margin-top: 15px;
    align-self: flex-end;
    padding: 10px 15px;
    background: none;
    border: 1px solid teal;
  }
</style>
