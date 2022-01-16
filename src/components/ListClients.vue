<template>
  <div class="container mt-2">
    <div class="row">
      <div class="col-md-12">
        <table class="table">
          <thead>
            <tr>
              <th>id</th>
              <th>Name</th>
              <th>Option</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody v-if="clients.length > 0">
            <tr v-for="client in clients" :key="client.id">
              <td>{{ client.id }}</td>
              <td v-if="currentClientId !== client.id">{{ client.name }}</td>
              <td v-if="currentClientId !== client.id">
                {{ client.option }}
              </td>
              <td v-if="currentClientId === client.id">
                <input
                  type="text"
                  minlength="2"
                  class="form-control"
                  v-model="client.name"
                />
              </td>
              <td v-if="currentClientId === client.id">
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
              </td>
              <td v-if="currentClientId !== client.id">
                <button
                  ref="btnEdit"
                  @click="editClient(client)"
                  class="btn btn-info m-1"
                >
                  Edit
                </button>
                <button
                  @click="deleteClient(client.id)"
                  class="btn btn-danger m-1"
                >
                  Delete
                </button>
              </td>
              <td v-else>
                <button
                  @click="updateClient(client)"
                  :disabled="client.name.length < 2"
                  class="btn btn-success m-1"
                >
                  Save
                </button>
                <button
                  @click="cancelEdit(client)"
                  class="btn btn-warning text-white m-1"
                >
                  Cancel
                </button>
              </td>
            </tr>
          </tbody>
          <p v-if="clients.length === 0">There isn't any client</p>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListClients",
  props: {
    clients: Array,
  },
  data() {
    return {
      currentClientId: null,
      currentClient: {},
    };
  },
  methods: {
    editClient(client) {
      Object.assign(this.currentClient, client);
      this.currentClientId = client.id;
    },
    updateClient(current) {
      //console.log("current: ", current);
      if (current.name.length < 2 || !current.option) {
        Object.assign(current, this.currentClient);
        this.currentClientId = null;
      }
      this.$emit("updateClient", current);
      this.currentClientId = null;
    },
    cancelEdit(client) {
      //console.log(this.currentClient);
      Object.assign(client, this.currentClient);
      this.currentClientId = null;
    },
    deleteClient(id) {
      //console.log("delete client ", id);
      let conf = confirm(
        `Are you sure? You want to delete client with id: ${id}`
      );
      if (conf) {
        this.$emit("deleteClient", id);
      } else {
        return null;
      }
    },
  },
};
</script>