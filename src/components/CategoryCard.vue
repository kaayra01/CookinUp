<template>
  <article class="category">
    <header class="category__header">
      <img
        :src="`/images/icons/categorias_ingredientes/${categoria.imagem}`"
        alt="Imagem relacionada à categoria do ingrediente"
        class="category__image"
      />
      <h2 class="paragraph-lg category__name">{{ categoria.nome }}</h2>
    </header>
    <ul class="category__ingredients">
      <li v-for="ingrediente in categoria.ingredientes" :key="ingrediente">
        <SelectableIngredient
          :ingrediente="ingrediente"
          @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
          @remover-ingrediente="$emit('removerIngrediente', $event)"
        />
      </li>
    </ul>
  </article>
</template>

<script lang="ts">
import type ICategory from "@/interfaces/ICategory";
import type { PropType } from "vue";
import Tag from "./Tag.vue";
import SelectableIngredient from "./SelectableIngredient.vue";

export default {
  components: {
    Tag,
    SelectableIngredient,
  },

  props: {
    categoria: {
      type: Object as PropType<ICategory>,
      required: true,
    },
  },

  emits: ["adicionarIngrediente", "removerIngrediente"],
};
</script>

<style scoped>
.category {
  width: 19.5rem;
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #fff);
  box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.category__header {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.category__image {
  width: 3.5rem;
}

.category__name {
  text-align: center;
  color: var(--verde-medio, #3d6d4a);
  font-weight: 700;
}

.category__ingredients {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  flex-wrap: wrap;
}
</style>
