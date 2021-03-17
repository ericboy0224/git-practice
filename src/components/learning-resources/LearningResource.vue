<template>
  <base-card>
    <li>
      <div>
        <header>
          <h3>{{ title }}</h3>
          <base-button mode="flat" @click="removeRes">刪除</base-button>
        </header>
        <p>{{ desc }}</p>
        <nav>
          <a :href="link">學習資源</a>
        </nav>
      </div>
    </li>
  </base-card>
</template>

<script>
export default {
  props: ["title", "desc", "link", "id"],
  inject: ["deleteResource"],
  methods: {
    removeRes() {
      this.deleteResource(this.id);
    }
  }
};
</script>
<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
