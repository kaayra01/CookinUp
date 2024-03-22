<template>
  <section class="select-ingredients">
    <h1 class="header ingredients-title">Ingredientes</h1>
    <p class="paragraph-lg instructions">
      Selecione abaixo os ingredientes que você quer usar nesta receita:
    </p>
    <ul class="categories">
      <li v-for="categoria in categorias" :key="categoria.nome">
        <CategoryCard
          :categoria="categoria"
          @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
          @remover-ingrediente="$emit('removerIngrediente', $event)"
        />
      </li>
    </ul>
    <p class="paragraph tip">
      *Atenção: Consideramos que você tem em casa sal, pimenta e água.
    </p>
    <MainButton text="Buscar receitas!" @click="$emit('buscarReceitas')" />
  </section>
</template>

<script lang="ts">
import { getCategories } from "@/http/index";
import type ICategory from "@/interfaces/ICategory";
import CategoryCard from "./CategoryCard.vue";
import MainButton from "./MainButton.vue";

export default {
  name: "SelectIngredients",

  components: {
    CategoryCard,
    MainButton,
  },

  data() {
    return {
      categorias: [] as ICategory[],
    };
  },

  async created() {
    this.categorias = await getCategories();
  },

  emits: ["adicionarIngrediente", "removerIngrediente", "buscarReceitas"],
};
</script>

<style scoped>
.select-ingredients {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.ingredients-title {
  color: var(--verde-medio, #3d6d4a);
  display: block;
  margin-bottom: 1.5rem;
}

.instructions {
  margin-bottom: 2rem;
}

.categories {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.tip {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .tip {
    margin-bottom: 2.5rem;
  }
}
</style>
