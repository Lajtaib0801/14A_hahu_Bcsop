<script setup lang="ts">
import { useStore } from "../stores/store";
const store = useStore();
</script>
<template>
  <q-page>
    <q-select
    v-model="store.many.document.categoryId"
    clearable
    color="green"
      emit-value
      label="Kategória"
      map-options
      option-label="categoryNameField"
      option-value="id"
      :options="store.one.documents"
      :rules="[(v) => v != null || 'Kérem válasszon kategóriát!']"
    />
  </q-page>
</template>

<style lang="scss" scoped>
h2 {
  font-size: 3vw;
}
</style>
