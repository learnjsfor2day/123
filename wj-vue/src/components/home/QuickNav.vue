/*library picture*/
<template>
  <div class="quick-nav">
    <img src="../../assets/img/icon/books.jpg" alt="" class="monster">
    <img src="../../assets/img/icon/book.jpg" alt="" class="readme">
  </div>
</template>

<script>
  export default {
    name: 'QuickNav'
  }
</script>

<style scoped>
  .quick-nav {
    width: 450px;
    height: 318px;
    background-color: transparent;
  }
  /*books location*/
  .monster {
    width: 880px;
    height: 150px;
    /*position: absolute;*/
    /*top: 150px;*/
    /*left: 700px;*/
  }
  /*book location*/
  .readme {
    width: 300px;
    height: 300px;
    position: absolute;
    margin-left: 44.5%;
    top: 241px;
    left: 230px;
  }

  .spark {
    position: absolute;
    margin-left: 50%;
    top: 100px;
    left: 20px;
  }

  .logo {
    width: 280px;
    position: absolute;
    margin-left: 50%;
    top: 50px;
    left: 210px;
  }

</style>
