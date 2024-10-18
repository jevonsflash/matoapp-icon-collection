<script setup lang="ts">
import Windows10 from '@/components/Axure Windows 10 Icon Library/index.html'
import Material from '@/components/Material Design Icon Library/index.html'
import { useRouter, onBeforeRouteUpdate } from "vue-router";
import { ref, onMounted } from "vue";
const type = ref<string | undefined>("");
const currentPath = ref<string | undefined>("");
const router = useRouter();

onMounted(() => {
  if (router.currentRoute.value.query["type"]) {
    type.value = router.currentRoute.value.query["type"].toString();
  } else {
    type.value = "";
  }
  initData();
});

onBeforeRouteUpdate((to) => {
  if (to.query["type"]) {
    type.value = to.query["type"].toString();
  } else {
    type.value = "";
  }
  initData();
});

function initData() {
  if (type.value === "md") {
    currentPath.value = Material;
  }
  else if (type.value === "win10") {
    currentPath.value = Windows10;
  }
}

</script>

<template>
  <main>
    <template v-if="type === ''">
      <div class="container">
        <h4>请选择一个图标库</h4>
      </div>
      <ul>
        <li><router-link to="/?type=win10">Axure Windows 10 Icon Library </router-link></li>
        <li><router-link to="/?type=md">Material Design Icon Library </router-link></li>
      </ul>
    </template>
    <template v-else>
      <iframe :src="currentPath" frameborder="0"></iframe>

    </template>
  </main>
</template>

<style scoped>
iframe {
  width: 100%;
  height: 75vh;
}
</style>