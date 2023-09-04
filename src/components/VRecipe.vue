<template>
  <div>
    <h2>{{ recipe.strMeal }}</h2>
    <img :src="recipe.strMealThumb" alt="">
    <p>{{ recipe.strInstructions }}</p>
    <ul>
      <li v-for="ingredient in ingredientsWithMeasure">
        {{ ingredient }}
      </li>
    </ul>
    <div class="gallery">
      <template v-for="ingredient in ingredients">
        <img :src="`https://www.themealdb.com/images/ingredients/${ingredient}.png`" alt="">
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "VRecipe",
  props: {
    recipe: {
      type: Object,
      default: null,
    },
  },
  computed: {
    ingredientsWithMeasure() {
      if (this.recipe) {

        console.log(Object.entries(this.recipe)
          .filter(([key, value]) => key.startsWith("strIngredient") && value?.trim()))

        return Object.entries(this.recipe)
          .filter(([key, value]) => key.startsWith("strIngredient") && value?.trim())
          .map(([key, value], index) => {
            const measureKey = `strMeasure${index + 1}`;
            const measureValue = this.recipe[measureKey];
            return this.formatIngredientWithMeasure(value, measureValue);
          });
      }
    },
    ingredients() {
      if (this.recipe) {
        return Object.entries(this.recipe)
          .filter(([key, value]) => key.startsWith("strIngredient") && value?.trim())
          .map(([_, value]) => value)
      }
    }
  },
  methods: {
    formatIngredientWithMeasure(ingredient, measure) {
      if (!ingredient) return ""; // Если нет ингредиента, возвращаем пустую строку
      if (!measure) return ingredient; // Если нет количества, возвращаем только ингредиент
      return `${ingredient} - ${measure}`;
    },
  }
}
</script>

<style scoped>
img {
  aspect-ratio: 16 / 9;
}
</style>
