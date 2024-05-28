

<script setup>
defineProps({
  image: String,
  name: String,
  status: String,
  species: String,
  location: Object,
  origin: Object
})


//если после выбора какого-то статуса вернуться ко всем карточкам, то все ломается, и только при обновлении страницы показывает все статусы
const getStatusClass = (status) => {
  switch (status) {
    case 'Alive':
      return 'green-circle';
    case 'Dead':
      return 'red-circle';
    case 'unknown':
      return 'yellow-circle';
    default:
      return '';
  }
};
</script>


<template>
<div class="wrapper-cards">
  <img :src="image" alt="">
  <div class="info">
    <div class="name">{{name}}</div>
    <div class="info-status">
      <span :class="getStatusClass(status)"></span>
      <div class="status">{{status}}</div>
      <div class="species">{{species}}</div>
    </div>
    <div class="location-block">
      <div class="location"><span class="location__title">Last known location:</span>{{location.name}}</div>
      <div class="origin"><span class="origin__title">First seen in:</span>{{origin.name}}</div>
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
.location-block{
  display: flex;
  flex-direction: column;
}
.location{
  margin-top: 20px;
  margin-left: 10px;
  font-size: 15px;
  display: flex;
  flex-direction: column;

}
.location__title{
  color: rgb(158, 158, 158);
  font-size: 14px;
  font-weight: bold;
}
.origin{
  margin-top: 20px;
  margin-left: 10px;
  font-size: 15px;
  display: flex;
  flex-direction: column;
}
.origin__title{
  color: rgb(158, 158, 158);
  font-size: 14px;
  font-weight: bold;
}
.circle{
  display: inline-block;
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
}

.green-circle{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(85, 204, 68)
}
.red-circle{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(214, 61, 46);
}
.yellow-circle{
  margin: 0 6px 0 10px;
  width: 8px;
  height: 8px;
  border-radius: 50px;
  background: rgb(214, 186, 46);
}
</style>