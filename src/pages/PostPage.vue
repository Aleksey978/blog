<script>
import PostForm from '../components/PostForm.vue';
import PostList from '../components/PostList.vue';
import MyButton from '../components/UI/MyButton.vue';
import MyDialog from '../components/UI/MyDialog.vue';
import axios from 'axios'
import MySelect from '../components/UI/MySelect.vue';
import MyInput from '../components/UI/MyInput.vue';
  export default {
    components: {
      PostForm,PostList,
        MyDialog,
        MyButton,
        MySelect,
        MyInput
    },
    data() {
      return {
        posts: [],
        dialoVisible: false,
        isPostLoading: false,
        selectedSort: '',
        searchQuery: '',
        page: 1,
        limit: 10,
        totalPage: 0,
        sortOptions: [
          {value: 'title', name: 'По названию'},
          {value: 'body', name: 'По описанию'},
        ]
      } 
    },
    methods: {
      createPost(post) {
        this.posts.push(post);
        this.dialoVisible = false;
      },
      removePost(post) {
        this.posts = this.posts.filter(p => p.id !== post.id)
      },
      showDialog() {
        this.dialoVisible = true
      },
      // changePage (pageNumber) {
      //   this.page = pageNumber
      //   this.fechPosts()
      // },
      async fechPosts() {
        try {
          this.isPostLoading = true;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          });
          this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = response.data;
        } catch (error) {
          alert('ошибка')
        } finally {
          this.isPostLoading = false;
        }
      },
      async loadMorePosts() {
        try {
          this.page += 1;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          });
          this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.posts = [...this.posts, ...response.data]
        } catch (error) {
          alert('ошибка')
        }
      },
    },
    mounted() {
      this.fechPosts();  
    },
    computed: {
      sortedPosts() {
        return [...this.posts].sort((post1, post2) => {
          return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
        })
      },
      sortedAndSearchedPosts() {
        return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
      }
    },
    // watch: {
    //   selectedSort(newVal) {
    //     this.posts.sort((post1, post2) => {
    //       return post1[newVal]?.localeCompare(post2[newVal])
    //     })
    //   }
    // }
  }
</script>

<template>
  <div>
    <h1>Старница с постами</h1>
    <my-input v-focus placeholder="Поиск..." v-model="searchQuery"/>
    <div class="app__btns">
      <my-button @click="showDialog">создать пост</my-button>
      <my-select v-model="selectedSort" :options="sortOptions"/>
    </div>    
    <my-dialog :show="dialoVisible"><PostForm @create="createPost"/></my-dialog>
      <PostList v-if="!isPostLoading" :posts="sortedAndSearchedPosts" @remove="removePost"/>
      <div v-else>Загрузка...</div>
      <div v-intersection="loadMorePosts" class="observer"></div>
      <!-- <div class="page__wrapper">
        <div 
        class="page"
        :class="{
          'current-page': page === pageNumber
        }"
        @click="changePage(pageNumber)"
         v-for="pageNumber in totalPage" 
         :key="pageNumber"
         >{{ pageNumber }}</div>
      </div> -->
  </div>
</template>

<style>
.app__btns {
  margin: 15px, 0;
  display: flex;
  justify-content: space-between;
}
.page__wrapper {
  display: flex;
  margin-top: 15px;
  justify-content: center;
}
.page {
  border: 1px solid teal;
  padding: 10px;
  cursor: pointer;
  margin-right: 10px;
}
.current-page {
  border: 2px solid red;
}
.observer {
  height: 30px;
}
</style>
