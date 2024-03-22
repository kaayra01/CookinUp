<template>
  <article class="recipe">
    <header class="recipe__header">
      <img
        :src="`/images/icons/receitas/${receita.imagem}`"
        alt="Imagem relacionada às receitas"
        class="recipe__image"
      />
    </header>
    <section class="recipe__body">
      <h2 class="paragraph recipe__name">{{ receita.nome }}</h2>
    </section>
  </article>
</template>

<script lang="ts">
import type IRecipe from "@/interfaces/IRecipe";
import type { PropType } from "vue";

export default {
  props: {
    receita: {
      type: Object as PropType<IRecipe>,
      required: true,
    },
  },
};
</script>

<style scoped>
.recipe {
  display: flex;
  width: 17.625rem;
  max-width: 19.5rem;
  flex-direction: column;
  align-items: center;
  border-radius: 1rem;
  background: var(--Branco, #fff);
  box-shadow: 4px 4px 12px 0px rgba(68, 68, 68, 0.08);
}

.recipe__body {
  padding: 2rem 1rem;
}

.recipe__image {
  width: 100%;
  border-radius: 1rem 1rem 0rem 0rem;
  display: block;
}

.recipe__name {
  font-weight: 700;
  color: var(--cinza, #444);
}
</style>
