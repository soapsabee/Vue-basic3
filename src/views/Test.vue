<template>
    <div>
        <h1>Google Store</h1>
        <b-form-group horizontal label="Search" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
        <b-table striped hover :items="products" :fields="fields" :filter="filter" :per-page="10" :current-page="pageIndex" @filtered="onFiltered">
        <template slot="actions" slot-scope="row">
        <!-- We use @click.stop here to prevent a 'row-clicked' event from also happening -->
        <b-button size="sm" @click.stop="info(row.item, row.index, $event.target)" class="mr-1">
          Info modal
        </b-button>
        
      </template>
   

        </b-table>
        <b-pagination size="md" :total-rows="products.length" v-model="pageIndex" :per-page="pageSize"></b-pagination>

    </div>
</template>
<script>
import axios from "axios";
export default {
  name: "product",
  components: {},
  data() {
    return {
      message: "Project 2",
      products: [],
      pageSize: 10,
      pageIndex: 1,
      fields: [
        {
          key: "id",
          sortable: true
        },
        {
          key: "title",
          sortable: true
        },
        {
          key: "price",
          sortable: true,
          variant: "danger"
        }
      ],
      filter: null,
    };
  },
  methods: {
    onFiltered (filteredItems) {
      // Trigger pagination to update the number of buttons/pages due to filtering
      this.totalRows = filteredItems.length
      this.currentPage = 1
    }
  },
  mounted() {
    var instance = this;
    axios
      .get("https://sleepy-reef-53571.herokuapp.com/api/products")
      .then(function(response) {
        console.log(response.data);
        instance.products = response.data.data;
      });
  }
};
</script>