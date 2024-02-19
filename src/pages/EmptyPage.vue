<script setup lang="ts">
import CardComponent from "src/components/CardComponent.vue";
import { useStore } from "src/stores/store";
import { ref } from "vue";
import { onMounted } from "vue";
const store = useStore();
const selectedCategoryName = ref(store.many.documents[0]);
onMounted(() => {
  store.getAllCategories();
  store.one_GetAll();
});
</script>
<template>
  <!-- <p v-for="(item, index) in store.one.documents" :key="index">{{ item }}</p> -->
  <q-page>
    <div class="row justify-center">
      <q-select
        v-model="selectedCategoryName"
        clearable
        emit-value
        label="Kategória"
        map-options
        option-label="categoryNameField"
        option-value="id"
        :options="store.many.documents"
        :rules="[(v) => v != null || 'Kérem válasszon kategóriát!']"
      ></q-select>
    </div>
    <div class="row justify-center q-ma-xl">
      <div v-for="(item, index) in store.many.documents" :key="index" class="col-xs-12 col-sm-6 col-md-4 col-lg-3">
        <CardComponent>{{ item }}</CardComponent>
      </div>
    </div>
  </q-page>
</template>

<style lang="scss" scoped></style>