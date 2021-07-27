<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid input">
    <template v-slot:default>
      <p>Input fields are invalid</p>
      <p>Please fill all the fields...</p>
    </template>
    <template v-slot:actions>
      <base-button @click="closeDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" ref="resTitle" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name=""
          rows="3"
          placeholder="add description"
          ref="resDescription"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" ref="resUrl" />
      </div>
      <div class="form-control">
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../../UI/BaseButton.vue';
export default {
  components: {
    BaseButton
  },
  inject: ['AddResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.resTitle.value;
      const enteredDescription = this.$refs.resDescription.value;
      const enteredLink = this.$refs.resUrl.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      this.AddResource(enteredTitle, enteredDescription, enteredLink);
    },
    closeDialog() {
      this.inputIsInvalid = false;
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
input,
text {
  height: 2rem;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #e5cbf7;
}

.form-control {
  margin: 1rem 0;
}
</style>
