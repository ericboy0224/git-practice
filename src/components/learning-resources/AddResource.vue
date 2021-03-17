<template>
  <teleport to="body">
    <base-dialog
      v-if="isInputInvalid"
      title="不正確的輸入行為"
      @close="confirmError"
    >
      <template #default>
        <p>輸入至少有一格空格未填入</p>
        <p>請確定填答完畢再進行新增</p>
      </template>
      <template #actions>
        <base-button @click="confirmError">我了解了</base-button>
      </template>
    </base-dialog>
  </teleport>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">標題</label>
        <input type="text" name="title" id="title" ref="inputTitle" />
      </div>
      <div class="form-control">
        <label for="desc">描述</label>
        <textarea name="desc" id="desc" rows="3" ref="inputDesc"></textarea>
      </div>
      <div class="form-control">
        <label for="link">網址</label>
        <input type="url" name="link" id="link" ref="inputUrl" />
      </div>
      <base-button>新增</base-button>
    </form>
  </base-card>
</template>
<script>
import BaseButton from "../UI/BaseButton.vue";
export default {
  components: { BaseButton },
  inject: ["addResource"],
  data() {
    return {
      isInputInvalid: false
    };
  },
  methods: {
    submitData() {
      const enterTitle = this.$refs.inputTitle.value;
      const enterDesc = this.$refs.inputDesc.value;
      const enterUrl = this.$refs.inputUrl.value;
      if (
        enterTitle.trim() === "" ||
        enterDesc.trim() === "" ||
        enterUrl.trim() === ""
      ) {
        this.isInputInvalid = true;
        return;
      }
      this.addResource(enterTitle, enterDesc, enterUrl);
    },
    confirmError() {
      this.isInputInvalid = false;
    }
  }
};
</script>
<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
