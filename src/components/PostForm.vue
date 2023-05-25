<template>
    <form @submit.prevent>
        <h4>создание поста</h4>
        <my-input v-focus v-model="post.title" placeholder="название поста"/>
        <my-input v-model="post.body" placeholder="описание поста"/>
        <!-- <button @click="createPost" class="btn">Создать пост</button> -->
        <my-button class="btnForm" @click="createPost">Создать</my-button>
      </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: "",
                body: ""
            }
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: "",

            };
        }
    },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
.btnForm {
  align-self: self-end;
}
</style>