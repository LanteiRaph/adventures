<template>
    <header id="pageHeader">
      <div class="header">
        <span class="logo">
          <p>Timchist adventures</p>
        </span>
        <span class="user">
          <router-link to='/cart'>
            <span> <img src="@/assets/busket.png" width="20px"/></span>
          </router-link>
          <router-link to="/login" class="link">
            <span class="btn">Login</span>
          </router-link>
          <router-link to="/login" class="link">
            <span class="btn">Sign Up</span>
          </router-link>
        </span>
      </div>
    </header>
</template>

<script>
export default {
  name: 'Header',
  data () {
    return {

    }
  }
}
</script>

<style scoped>

</style>
