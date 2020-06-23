<template>
<div>
    <a href="#top" class="box">
      <a-icon type="caret-up" />
  </a>
</div>
  
</template>

<script>
export default {

}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.box{
    width: 30px;
    height: 30px;
    background: #FADB14;
    border-radius: 5px;
    padding: 4px 7px;
    position: fixed;
    bottom: 8px;
    right: 8px;
    z-index: 3;
    border: 1px solid #bba410;
    transition: 0.3s;
}

.box:hover{
    background-color: #bba410;
}

a{
    color: #262626;
}
</style>