<template>
  <base-dialog @close="confirmError" v-if="isFormInvalid" title="Invalid input">
    <template #default>
      <p>Unfortunately, one or more inputs are invalid</p>
      <p>
        Check all inputs, and make sure u added at least a few characters to
        each input
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input ref="title" type="text" id="title" name="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          ref="description"
          type="text"
          id="description"
          name="description"
          rows="3"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input ref="link" type="url" id="link" name="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return { isFormInvalid: false };
  },
  methods: {
    confirmError() {
      this.isFormInvalid = false;
    },
    submitData() {
      const enteredTitle = this.$refs.title.value;
      const enteredDescription = this.$refs.description.value;
      const enteredLink = this.$refs.link.value;

      if (enteredTitle == '' || enteredDescription == '' || enteredLink == '') {
        this.isFormInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
  },
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
