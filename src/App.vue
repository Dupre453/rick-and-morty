<script setup>
import {onMounted, reactive, ref, watch} from "vue";
import axios from "axios";
import debounce from 'lodash.debounce'
import CardList from "./components/CardList.vue"



const characters = ref([]) //{value: []}
const currentPage = ref(1)
const totalPages = ref(0);
const filters = reactive({
  status: '',
  searchCharacters: '',
})
const onChangeSelect = (event) => {
  filters.status = event.target.value
}
const onChangeSearchInput = debounce((event) => {
  filters.searchCharacters = event.target.value
}, 200)


const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    fetchCharacters();
  }
}

const previousPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    fetchCharacters();
  }
}

const fetchCharacters = async () => {
    try{
      const params = {
        status: filters.status,
      }
      if(filters.searchCharacters) {
        params.name = `${filters.searchCharacters}`
      }
      const {data} = await axios.get(
          `https://rickandmortyapi.com/api/character/?page=${currentPage.value}`,
          {
            params,
          },

      )
      characters.value = data.results
      totalPages.value = data.info.pages;
    }catch (error) {
      console.log(error)
    }
}


//при монтировании вызови запрос
onMounted(fetchCharacters)

//при изменении фильтрации вызови запрос
watch(filters, fetchCharacters)

</script>

<template>

    <div class="wrapper">

      <div class="home">
        <div class="logo">
          <img  src="./assets/rick-and-morty-31015.png" alt="logo">
        </div>

        <div class="filter-block">
          <select @change="onChangeSelect" class="select">
            <option value="">All</option>
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
        <div class="btn-block">
          <div class="buttons">
            <button @click="previousPage" class="btn"><</button>
            <button @click="nextPage" class="btn">></button>
          </div>
          <span class="counter">{{ currentPage }}/42</span>
        </div>

        <CardList :characters="characters"/>



      </div>
    </div>
</template>

<style scoped>
.wrapper{
  margin: 20px 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 25px;
}
.logo{
  margin: 30px;
  display: flex;
  justify-content: center;
  font-size: 34px;
  font-weight: bold;
}

img{
  border-radius: 10px 0 0 10px;
}



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
option{

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
.counter{
  font-size: 16px;
  font-weight: bold;
  margin:5px 0 0  5px;
  color: #f2f2f2;

}
.btn-block{
  display: flex;
  flex-direction: column;
  margin-left: 20px;
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
