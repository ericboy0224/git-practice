<template>
  <base-card>
    <base-button
      @click="selectComponent('stored-resource')"
      :mode="selectStoredResource"
      >資源</base-button
    >
    <base-button
      @click="selectComponent('add-resource')"
      :mode="selectAddResource"
      >加入</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import AddResource from "./AddResource.vue";
import StoredResource from "./StoredResource.vue";
export default {
  components: { AddResource, StoredResource },
  data() {
    return {
      selectedTab: "stored-resource",
      storedResources: [
        {
          id: "officail-guide",
          title: "官方學習教材",
          desc: "這是一個 Vue.js 的官方教材",
          link: "https://vuejs.org"
        },
        {
          id: "google",
          title: "Google",
          desc: "人人都該學會的最強自學工具",
          link: "https://google.com/"
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource
    };
  },
  methods: {
    selectComponent(cmp) {
      this.selectedTab = cmp;
      //   console.log(this.selectedTab);
    },
    addResource(title, desc, url) {
      const newRes = {
        id: new Date().toISOString(),
        title: title,
        desc: desc,
        link: url
      };
      this.storedResources.unshift(newRes);
      this.selectedTab = "stored-resource";
    },
    deleteResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id == resId);
      this.storedResources.splice(resIndex, 1);
    }
  },
  computed: {
    selectStoredResource() {
      return this.selectedTab === "stored-resource" ? null : "flat";
    },
    selectAddResource() {
      return this.selectedTab === "add-resource" ? null : "flat";
    }
  }
};
</script>
