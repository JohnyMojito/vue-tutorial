<template>
  <div class="col-sm-6 col-md-4">
      <div class="card text-white bg-success mb-3">
        <div class="card-header bg-danger">
          <h3 class="card-title">
            {{ stock.name }}
            <small>(Price: {{ stock.price }})</small>
          </h3>
        </div>
        <div class="card-body">
          <div>
            <input 
              type="number"
              class="form-control"
              placeholder="Quantity"
              v-model="quantity"
              :class="{danger: insufficientFunds}"
            />
          </div>
          <div class="mt-2">
            <button
              class="btn btn-outline-light"
              @click="buyStock"
              :disabled="quantity <= 0 || insufficientFunds"
            >
              {{ insufficientFunds ? 'Insufficient Funds' : 'Buy'}}
            </button>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0,
    };
  },
  computed: {
    funds(){
      return this.$store.getters.funds
    },
    insufficientFunds() {
      return this.quantity*this.stock.price > this.funds
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.$store.dispatch("buyStock", order);
      this.quantity = null;
    },
  },
};
</script>

<style scoped>
.danger {
  border: 1px solid red;
}
</style>