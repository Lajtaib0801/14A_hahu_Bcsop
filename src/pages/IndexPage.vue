<script setup lang="ts">
// import CardComponent from "src/components/CardComponent.vue";
import { useStore } from "src/stores/store";
import { ref } from "vue";
import { onMounted } from "vue";
const store = useStore();
const selectedCategoryName = ref(store.one.documents[0]);
let toggled = ref(false);

const longText = ref("");
let displayText = ref("");
onMounted(() => {
  store.getAllCategories();
  store.one_GetByCategory(selectedCategoryName?.value?.categoryNameField || "Személyautó");
});

console.log(store.many.cars);


const handleToggle = (toggled) => {
  if (!toggled) {
    let slicedText = "";
    let lastWhiteSpaceIdx = -1;
    for (let index = 0; index < 100; index++) {
      slicedText += longText.value[index];
      if (longText.value[index] == " ") {
        lastWhiteSpaceIdx = index;
      }
    }
    if (slicedText[99] == " ") {
      displayText.value = slicedText.slice(0, 98) + "...";
    } else {
      displayText.value = slicedText.slice(0, lastWhiteSpaceIdx) + "...";
    }
  } else {
    displayText.value = longText.value;
  }  
};
</script>
<template>
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
      <div v-for="(item, index) in store.many.cars" :key="index" class="col-xs-12 col-sm-6 col-md-4 col-lg-3">
        <q-card bordered class="q-ma-md" flat>
          <q-card-section class="text-center text-h5" style="background-color: rgb(200, 190, 156)">
            {{ item.cim }} - {{ item.vetelar }}
          </q-card-section>
          <q-card-section class="text-h7" style="background-color: rgb(255, 228, 196)">
            <ul>
              <li>
                <span>Szin: </span><b>{{ item.szin }}</b>
              </li>
              <li>
                <span>Évjárat: </span><b>{{ item.evjarat }}</b>
              </li>
              <li>
                <span>Hengerűrtartalom: </span><b>{{ item.hengerurtartalom }}</b>
              </li>
              <li>
                <span>Hirdetés dátuma: </span><b>{{ item.hirdetes_datum }}</b>
              </li>
            </ul>
          </q-card-section>
          <q-card-section class="" style="background-color: rgb(200, 190, 156)">
            <div class="text-h7 text-justify">{{ item.leiras }}</div>
            <hr />
            <q-toggle
              v-model="toggled"
              color="dark-blue"
              :disable="longText.length <= 100"
              label="Teljes hirdetés"
              @update:model-value="handleToggle"
            />
          </q-card-section>
          <q-card-section style="background-color: rgb(255, 228, 196)">
            <q-img role="img" :src="item.kepek?.[0]" style="max-height: 200px"></q-img>
          </q-card-section>
          <q-card-section style="background-color: rgb(200, 190, 156)">
            <div class="text-h7 text-justify">{{ item.kepek?.[0] }}</div>
          </q-card-section>
          <q-card-actions class="justify-center" style="background-color: rgb(255, 228, 196)">
            <q-btn class="bg-green-3" label="Hirdetés szerkesztése" no-caps type="button"></q-btn>
          </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<style lang="scss" scoped></style>
