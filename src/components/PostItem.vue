<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    }
  }
}
</script>

<template>
  <div class="post">
    <div>
      <div>{{ post.id }}</div>
      <div class=""><strong>Название: </strong>{{ post.title }}</div>
      <div class=""><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <div class="post__btns">
      <my-button class="post__btn" @click="$router.push(`/posts/${post.id}`)">Открыть</my-button>
      <my-button class="post__btn" @click="$emit('remove', post)">удалить</my-button>
    </div>
  </div>
</template>

<style>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.post__btns {
  display: flex;
  justify-content: space-between;
}
.post__btn {
  margin-left: 10px;
}
</style>