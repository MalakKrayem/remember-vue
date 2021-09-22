<template>
  <BaseDialoag v-if="inputIsInvalid" title="Invalid Input" @close="close">
    <template #default>
      <p>Oh, at least one input value is invalid</p>
      <p>
        Please check your input and enter at least a few chrachter into each
        input feild
      </p>
    </template>
    <template #actions>
      <BaseButton @click="close">Okay</BaseButton>
    </template>
  </BaseDialoag>
  <BaseCard>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
</template>

<script>
import BaseCard from "@/components/UI/BaseCard.vue";
import BaseButton from "@/components/UI/BaseButton.vue";
import BaseDialoag from "@/components/UI/BaseDialoag.vue";
export default {
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  components: {
    BaseCard,
    BaseButton,
    BaseDialoag,
  },
  inject: ["addResource"],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === "" ||
        enteredDescription.trim() === "" ||
        enteredUrl.trim() === ""
      ) {
        this.inputIsInvalid = true;
      } else {
        this.addResource(enteredTitle, enteredDescription, enteredUrl);
      }
    },
    close() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style lang="scss" scoped>
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
