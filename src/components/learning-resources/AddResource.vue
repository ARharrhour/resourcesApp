<template>
  <base-dialog
    @close="ConfirmError"
    v-if="inptsIsInvalid"
    title="Invalid Input"
  >
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template v-slot:actions>
      <base-button @click="ConfirmError">Okay</base-button>
    </template></base-dialog
  >
  <base-card>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="text" ref="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="description"
        >
        </textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" ref="link" />
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
    return {
      inptsIsInvalid: false,
    };
  },
  methods: {
    submitResource() {
      const enteredTitle = this.$refs.title.value;
      const enteredDescription = this.$refs.description.value;
      const enteredURL = this.$refs.link.value;
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredURL.trim() === ''
      ) {
        this.inptsIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredURL);
    },
    ConfirmError() {
      this.inptsIsInvalid = false;
    },
  },
};
</script>
<style>
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
