<template>
  <form @submit.prevent="sendForm">
    <div class="form-group">
      <label for="client-name">Name: </label>
      <input
        class="form-control"
        type="text"
        id="client-name"
        v-model="client.name"
        required
      />
    </div>
    <div class="form-group">
      <label for="client-options">Options: </label>
      <select
        class="form-control"
        name=""
        id=""
        v-model="client.option"
        title="Options"
        required
      >
        <option selected value="" disabled>Select option</option>
        <option value="Active">Active</option>
        <option value="Inactive">Inactive</option>
        <option value="Debtor">Debtor</option>
      </select>
    </div>
    <div class="text-center">
      <button
        type="sumbit"
        class="btn btn-info"
        :disabled="!client.name || !client.option"
      >
        Submit
      </button>
    </div>
  </form>
</template>

<script>
export default {
  name: "FormClients",
  emits: ["addClient"],
  data() {
    return {
      client: {
        name: "",
        option: "",
      },
    };
  },
  methods: {
    sendForm() {
      this.$emit("addClient", this.client);
    },
  },
};
</script>