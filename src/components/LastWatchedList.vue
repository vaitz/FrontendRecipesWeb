<template>
  <b-container>
    <h3 class="title">
      {{ title }}:
      <slot></slot>
    </h3>
    <b-card-group>
      <span v-for="r in recipes" :key="r.id">
        <RecipePreview width="20rem" class="recipePreview" :recipe="r" />
        <br />
      </span>
    </b-card-group>
  </b-container>
</template>

<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      recipes: [],
    };
  },
  mounted() {
    this.updateRecipes();
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.get(
          "http://localhost:3100/users/lastWatched"
        );

        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
.title {
  padding-bottom: 5%;
  margin-left: 2%;
  color: rgb(255, 254, 244);
  font-size: 40px;
  font-weight: bold;
  text-shadow: 2px 2px 4px #000000;
}
</style>
