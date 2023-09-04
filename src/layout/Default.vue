<template>
  <div class="container">
    <VBtn @click="fetchRandomRecipe" :loading="loading"/>
    <VRecipe v-if="clicked" :recipe="recipe"/>
  </div>
</template>

<script>
import VBtn from "../components/VBtn.vue";
import VRecipe from "../components/VRecipe.vue";

export default {
  name: "Default",
  components: {VRecipe, VBtn},
  data() {
    return {
      recipe: null, // Здесь будет храниться объект с информацией о рецепте
      loading: false, // Флаг для отображения состояния загрузки
      error: '', // Сообщение об ошибке, если запрос не удался
      clicked: false
    };
  },

  methods: {
    fetchRandomRecipe() {
      const url = 'https://www.themealdb.com/api/json/v1/1/random.php';
      this.loading = true

      fetch(url).then((response) => {
        if (response.ok) {
          return response.json();
        } else {
          throw new Error('Error: Failed to fetch data from the API.');
        }
      }).then((data) => {
        console.log(data.meals[0])
        this.recipe = data.meals[0];
        this.loading = false; // Загрузка завершена
        this.clicked = true
      }).catch((error) => {
        this.error = error.message;
        this.loading = false; // Загрузка завершена
      });
    },


  },
}
</script>

<style scoped>

</style>
