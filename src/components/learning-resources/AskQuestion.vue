<template>
  <base-dialog v-if="invalidInput" title="Invalid Input" @close="confirmAlert">
    <template #default>
      <p>It appears you have left the field blank.</p>
      <p>
        Please feel free to reference the existing responses for inspiration!
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmAlert">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="prompt">Please enter a question:</label>
        <textarea name="prompt" id="prompt" rows="3" ref="promptInput"></textarea>
      </div>
      <div>
        <base-button type="submit">Submit</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: {
    BaseDialog
  },
  inject: ['askQuestion'],
  data() {
    return {
      invalidInput: false
    };
  },
  methods: {
    submitData() {
      const enteredPrompt = this.$refs.promptInput.value;

      if (
        enteredPrompt.trim() === '' 
      ) {
        this.invalidInput = true;
        return;
      }

      this.askQuestion(enteredPrompt);
    },
    confirmAlert() {
      this.invalidInput = false;
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

.form-control:first-child {
  margin-top: 0rem;
}
</style>
