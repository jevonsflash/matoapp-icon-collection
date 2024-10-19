<script setup lang="ts">
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
    currentPath.value = "Material Design Icon Library";
  }
  else if (type.value === "win10") {
    currentPath.value = "Axure Windows 10 Icon Library";
  }
  else if (type.value === "slack") {
    currentPath.value = "Slack Axure Icon Library";
  }
  else if (type.value === "fa5") {
    currentPath.value = "Font Awesome 5.12 Axure Widget Library";
  }
  else if (type.value === "ad") {
    currentPath.value = "Ant Design System Icon Library";
  }
  else if (type.value === "ibm") {
    currentPath.value = "IBM Carbon Design System Axure Icon Library";
  }
  else if (type.value === "brand") {
    currentPath.value = "Brand Icons v3";
  }
  else if (type.value === "bs") {
    currentPath.value = "Bootstrap Icon Library (v1.8.0)";
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
        <li><router-link to="/?type=slack">Slack Axure Icon Library </router-link></li>
        <li><router-link to="/?type=fa5">Font Awesome 5.12 Axure Widget Library </router-link></li>
        <li><router-link to="/?type=ad">Ant Design System Icon Library </router-link></li>
        <li><router-link to="/?type=ibm">IBM Carbon Design System Axure Icon Library </router-link></li>
        <li><router-link to="/?type=brand">Brand Icons v3 </router-link></li>
        <li><router-link to="/?type=bs">Bootstrap Icon Library (v1.8.0) </router-link> </li>
      </ul>
    </template>
    <template v-else>
      <h4>{{ currentPath }}</h4>
      <iframe :src="currentPath+'/index.html'" frameborder="0"></iframe>

    </template>
  </main>
</template>

<style scoped>
iframe {
  width: 100%;
  height: 75vh;
}
</style>