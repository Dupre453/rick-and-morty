

<script setup>

defineProps({
  nextPage: Function,
  previousPage: Function,
  currentPage: Number
})


</script>


<template>
  <div class="btn-block">
    <div class="buttons">
      <button @click="previousPage" class="btn"><</button>
      <button @click="nextPage" class="btn">></button>
    </div>
    <span class="counter">{{ currentPage }}/42</span>
  </div>
</template>


<style scoped>
.counter{
  font-size: 16px;
  font-weight: bold;
  margin:5px 0 0  5px;
  color: #39a49b;

}
.btn-block{
  display: flex;
  flex-direction: column;
  margin-left: 20px;
  margin-top: 20px;
}
.buttons{
  width: 90px;
  display: flex;

  justify-content:space-between;

}
.btn{
  cursor: pointer;
  padding: 10px 15px;
  border-radius: 50px;
  border:1px solid #39a49b;
  background: rgb(60, 62, 68);
  color: #39a49b;
  -webkit-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  -moz-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
}
</style>