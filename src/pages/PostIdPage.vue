<script>
import PostItem from '../components/PostItem.vue';
import axios from 'axios';
import PostIdItem from '../components/PostIdItem.vue';
export default {
  components: { PostItem, PostIdItem },
  data() {
    return {
      singlePost: {
        id: null,
        title: "",
        body: ""
      }
    };
  },
  props: {
    posts: {
      type: Array,
      required: true,
    }
  },
  methods: {
    async fechIdPosts() {
        try {
          const postId = this.$route.params.id;
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}`);
          this.post = response.data;
          // console.log(this.post.title);
          console.log(this.singlePost.title);
          this.singlePost.title = this.post.title;
          this.singlePost.body = this.post.body;
          // this.title = this.post.title
        } catch (error) {
          alert('ошибка')
        }
      },
  },
  mounted() {
      this.fechIdPosts(); 
    },
}

</script>

<template>
  <div>
    <h1>Страница поста с id = {{ $route.params.id }}</h1>
    <post-id-item :post="singlePost"></post-id-item>
    <!-- получаем параметры из роута, а именно id -->
    <!-- <post-item :post="singlePost"></post-item> -->
  </div>
</template>

<style>

</style>