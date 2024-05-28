<script setup>

defineProps({
  onChangeSearchInput: Function,
  onChangeSelect: Function
})

</script>

<template>
  <div class="filter-block">
    <select @change="onChangeSelect" class="select">
      <option value="all">All</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>

    <div class="search-block">
      <input
          @input="onChangeSearchInput"
          class="search-input" type="text"  placeholder="Search character">
    </div>
  </div>
</template>



<style scoped>
.filter-block{
  display: flex;
  justify-content: end;

}
.select{
  outline: none;
  -webkit-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  -moz-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  background: rgb(60, 62, 68);
  border:1px solid #39a49b;
  padding: 0 10px;
  border-radius: 20px;
  color: #f2f2f2;
  font-weight: bold;
}
.search-block{
  display: flex;
  position: relative;
  justify-content: center;
  margin-left: 30px;
}
.search-input{

  border:1px solid #39a49b;
  background: transparent;
  padding: 10px 20px;
  border-radius: 30px;
  outline: none;
  color: #bccc2b;
  font-size: 16px;
  width: 300px;
  -webkit-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  -moz-box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
  box-shadow: 0 10px 20px -4px rgba(63, 213, 188, 0.26);
}
.search-input::placeholder{
  color: #39a49b;
  opacity: 0.4;
}
option{
  padding: 10px;
}
</style>