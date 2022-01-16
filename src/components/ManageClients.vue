<template>
  <main class="container-fluid mt-3">
    <h1 class="text-center">
      Manage Clients <i class="far fa-address-book"></i>
    </h1>
    <div class="row">
      <div class="col-md-12 mt-2">
        <p class="text-center font-weight-bold text-primary">
          Add client <i class="fas fa-user-plus"></i>
        </p>
        <FormClients @addClient="addClient" />
        <div
          :class="`alert alert-${msg[1]} fade show mt-2`"
          role="alert"
          v-if="msg"
        >
          {{ msg[0] }}
        </div>
      </div>
      <div class="col-md-12 mt-4">
        <p class="text-center font-weight-bold text-primary">
          List of clients <i class="fas fa-list-ul"></i>
        </p>
        <ListClients
          :clients="clients"
          @updateClient="updateClient"
          @deleteClient="deleteClient"
        />
      </div>
    </div>
  </main>
</template>

<script>
import FormClients from "./FormClients.vue";
import ListClients from "./ListClients.vue";

export default {
  name: "ManageClients",
  components: {
    FormClients,
    ListClients,
  },
  data() {
    return {
      clients: [
        {
          id: 1,
          name: "Diego",
          option: "Active",
        },
        {
          id: 2,
          name: "Joel",
          option: "Inactive",
        },
      ],
      msg: null,
    };
  },
  methods: {
    addClient(client) {
      //console.log("padre", client.name + " " + client.option);
      //console.log(this.clients.length);
      if (this.clients.length === 0) {
        this.clients.push({ id: 0, ...client });
        //console.log("length 0 ", this.clients);
      } else {
        this.clients.push({
          id: this.clients[this.clients.length - 1].id + 1,
          ...client,
        });
        //console.log("length nueva: ", this.clients.length, this.clients);
      }
      this.msg = ["Client added", "success"];
    },
    updateClient(client) {
      //console.log("up ", client);
      //console.log("all1 ", this.clients);
      this.clients = this.clients.map((el) => {
        return el.id === client.id ? client : el;
      });
      this.msg = ["Client updated", "info"];
      //console.log("all2", this.clients);
    },
    deleteClient(id) {
      //console.log("The id is: ", id);
      this.clients = this.clients.filter((el) => {
        return el.id !== id;
      });
      this.msg = ["Client deleted", "danger"];
      //console.log("new:", this.clients);
    },
  },
};
</script>