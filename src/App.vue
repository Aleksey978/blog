<script>
import NavBar from './components/NavBar.vue'
export default {
  components: { NavBar },

}
</script>

<template>
	<div>
		<nav-bar></nav-bar>
  <div class="app">
    <router-view></router-view>
  </div>
	</div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 15px;
}
</style>