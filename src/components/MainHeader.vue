<template>
    <header class="main-header">
        <h1>miaomiao代办事项</h1>
    </header>
</template>

<script>
export default {
    name:'MainHeader'
}
</script>

<style scoped>
@import '../assets/style/color.css';

@font-face {
  font-family: '千图雪花体';
  src: url('../assets/千图雪花体.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
}

.main-header{
    text-align: center;
  font-family: '千图雪花体', sans-serif;
}
h1{
    margin:20px;
    font-size:70px;
    font-weight:100;
    color:rgb(161, 169, 241);
    text-shadow:5px 5px 5px rgba(0,0,0,0.1);
}
</style>


<!-- 千图雪花体.ttf -->
