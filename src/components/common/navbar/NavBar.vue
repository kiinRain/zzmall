<template>
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
   
  </div>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>

<style>
.nav-bar{
  display: flex;
  line-height: 44px;
  text-align: center;
  box-shadow: 0 1px 1px rgba(100, 100, 100, .1);
  z-index: 99;
}
.left,.right{
  /* background: rgb(143, 143, 143); */
  height: 44px;
  width: 60px;
}
.center{
  flex: 1;
  /* background: hotpink; */
}
</style>