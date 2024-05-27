

<script setup>
defineProps({
  image: String,
  name: String,
  status: String,
  species: String,
})
</script>


<template>
<div class="wrapper-cards">
  <img :src="image" alt="">
  <div class="info">
    <div class="name">{{name}}</div>
    <div class="info-status">
      <span class="yellow"></span>
      <div class="status">{{status}}</div>
      <div class="species">{{species}}</div>
    </div>
  </div>
</div>
</template>

<style scoped>
.wrapper-cards{
  background: rgb(60, 62, 68);
  border-radius: 10px;
  display: flex;
  width: 600px;
  height: 220px;
  border: 1px solid #39a49b;
  -webkit-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  -moz-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
}
.info{
  display: flex;
  flex-direction: column;
  padding: 12px;
  color:rgb(245, 245, 245);
}
.name{
  margin-left: 10px;
  font-size: 24px;
  font-weight: bold;
}
.info-status{
  display: flex;
  font-weight: bold;
  align-items: center;
  font-size: 14px;
}
.status{
  font-weight: bold;
}
.status::after{
  content: '-';
  padding: 2px;
  font-weight: bold;
}
.species{
  font-weight: bold;
}
span, .green{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(85, 204, 68);
}
span, .red{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(214, 61, 46);
}
span, .yellow{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(214, 186, 46);
}
</style>