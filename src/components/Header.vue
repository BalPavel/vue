<template>
  <div class="header">
      <router-link to="/" class="header-menubutton">
        Главная
      </router-link>
      <router-link to="/about" class="header-menubutton">
        О сайте
      </router-link>
  </div>
</template>

<script>
export default {
  
}
</script>

<style lang="scss" scoped>
  .header {
    display: flex;
    justify-content: space-between;
    background: #ccc;
    border: 1px solid #333;
    width: 50%;
  }
  .header-menubutton {
    background: #bbb;
    border-radius: 10px;
    margin: 8px;
    padding: 8px;
    border: solid 1px #000;
  }
  .header-logoimg {
    width: 20px;
    height: 20px;
  } 
</style>