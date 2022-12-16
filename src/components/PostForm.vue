<template>
    <h3>Создание поста</h3>
    <form class="form" @submit.prevent>
      <MyInput 
        v-model="post.title"
        @input="post.title = $event.target.value"  
        type="text" 
        placeholder="Название"/>
      <MyInput 
        v-model="post.body"
        @input="post.body = $event.target.value" 
        class="input" 
        type="text" 
        placeholder="Описание"/>
      <MyButton
        style="align-self: flex-end; margin-top: 15px" 
        class="btn" 
        @click="createPost">Создать</MyButton>
    </form>
</template>

<script>
    export default {
        name: 'PostForm',
        data() {
            return {
                post: {
                    id: '',
                    title: '',
                    body: ''
                }
            }
        },
        methods: {
            createPost() {
                this.post.id = Date.now()
                this.$emit('create', this.post)
                this.post = {
                    title: '',
                    body: ''
                }
            }
        }
    }
</script>

<style scoped>
  .form {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
  }
</style>