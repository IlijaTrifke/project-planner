<template>
  <nav class="main-nav">
    <RouterLink :to="{ name: 'home' }">Projects</RouterLink>
    <RouterLink :to="{ name: 'addproject' }">Add a New Project</RouterLink>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #5f5a5a;
  font-size: 18px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>
