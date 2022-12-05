<template>
    <form class="form" @submit.prevent>
      <input 
        v-model="post.title"
        @input="post.title = $event.target.value" 
        class="input" 
        type="text" 
        placeholder="Название">
      <input 
        v-model="post.body"
        @input="post.body = $event.target.value" 
        class="input" 
        type="text" 
        placeholder="Описание">
      <MyButton
        style="align-self: flex-end; margin-top: 15px" 
        class="btn" 
        @click="createPost">Создать</MyButton>
    </form>
</template>

<script>
    import MyButton from "@/components/UI/MyButton.vue"
    export default {
        name: 'PostForm',
        components: {
            MyButton
        },
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

  .input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
  }
</style>