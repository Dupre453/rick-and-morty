<script setup>
import {onMounted, reactive, ref, watch} from "vue";
import debounce from 'lodash.debounce'
import axios from "axios";

import CardList from "./components/CardList.vue"
import Pagination from "@/components/Pagination.vue";
import FilterBlock from "@/components/FilterBlock.vue";


const characters = ref([])
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


onMounted(fetchCharacters)

watch(filters, fetchCharacters)

</script>


<template>
  <div class="wrapper">
    <div class="home">
      <div class="logo">
        <img src="./assets/rick-and-morty-31015.png" alt="logo">
      </div>
      <FilterBlock :onChangeSelect="onChangeSelect" :onChangeSearchInput="onChangeSearchInput"/>
      <Pagination :previousPage="previousPage" :nextPage="nextPage" :currentPage="currentPage"/>
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
</style>
