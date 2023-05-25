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
  <div class="post__id">
    <h4 class="post__id__title">{{ post.title }}</h4>
    <p class="post__id__body">{{ post.body }}</p>
  </div>
</template>

<style>
  .post__id {
    display: flex;
    align-items: center;
    flex-direction: column;
    text-align: center;
  }
  .post__id__title {
    font-size: 50px;
  }
  .post__id__body {
    font-size: 45px;
  }
</style>