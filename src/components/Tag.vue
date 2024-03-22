<template>
  <span :class="['tag', { active }]">
    {{ text }}
  </span>
</template>

<script lang="ts">
export default {
  props: {
    text: { type: String, required: true },
    active: Boolean,
  },
};
</script>

<style scoped>
.tag {
  display: inline-block;
  border-radius: 0.5rem;
  min-width: 4.25rem;
  padding: 0.5rem;
  text-align: center;
  transition: 0.2s;
  color: var(--cinza, #444);
  background: var(---cinza-claro, #efefef);
  font-weight: 400;
}

.tag.active {
  color: var(--creme, #fffaf3);
  background: var(--coral, #f0633c);
  font-weight: 700;
}
</style>
