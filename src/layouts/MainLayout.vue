<script setup lang="ts">
import { ref } from "vue";

let showMenuBar = ref(true);
</script>

<template>
  <q-layout view="hHh LpR fFf">
    <!-- Fejléc -->
    <q-header v-model="showMenuBar" class="bg-primary text-white" elevated>
      <q-toolbar>
        <q-toolbar-title class="toolbar-title-fontsize">
          Dolgozat minta
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
    <!-- A router ide (router-view) tölti be az oldalt -->
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<style lang="scss">
.active {
  background-color: #dddddd;
}

.toolbar-title-fontsize {
  font-size: 30px;
}
</style>
