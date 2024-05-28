
<script setup>
import Card from './Card.vue'


defineProps({
  characters: Array
})
</script>



<template>
  <div class="content" >
    <Card
        v-for="character in characters"
        :key="character.id"
        :image="character.image"
        :name="character.name"
        :status="character.status"
        :species="character.species"
    />

  </div>
</template>

<style scoped>
.content{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 30px;
  justify-content: center;
  padding:30px 0 72px;
}
</style>