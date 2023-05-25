<script>

export default {
 
}
</script>

<template>
<div class="navbar">
  <div @click="$router.push('/')">Vue 3</div>
  <div class="navbar__btns">
    <my-button @click="$router.push('/posts')" class="navbar__btn">Посты</my-button>
    <my-button @click="$router.push('/about')" class="navbar__btn">Обо мне</my-button>
  </div>

</div>
</template>

<style>
.navbar {
  height: 50px;
  background-color: rgb(145, 145, 145);
  box-shadow: 2px 2px 4px gray;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 15px;
}
.navbar__btn {
  margin-right: 10px;
}
</style>