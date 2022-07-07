<template>
  <div class="container">
    <table class="table table-hover table-primary">
      <thead>
        <tr>
          <th>
            <h1>Valet</h1>
          </th>
          <th>
            <h1>in</h1>
          </th>
          <th>
            <h1>out</h1>
          </th>
          <th>
            <h1>h</h1>
          </th>
          <th>
            <h1>tips</h1>
          </th>
          <th>
            <h1></h1>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(invoice_product, k) in invoice_products" :key="k">
          <td>
            <input
              class="form-control"
              type="text"
              v-model="invoice_product.product_name"
            />
          </td>
          <td>
            <input
              class="form-control text-right"
              type="number"
              min="0"
              step=".01"
              v-model="invoice_product.product_price"
              @change="calculateLineTotal(invoice_product)"
            />
          </td>
          <td>
            <input
              class="form-control text-right"
              type="number"
              min="0"
              step=".01"
              v-model="invoice_product.product_qty"
              @change="calculateLineTotal(invoice_product)"
            />
          </td>
          <td>
            <input
              readonly
              class="form-control text-right"
              type="number"
              min="0"
              step=".01"
              v-model="invoice_product.line_total"
            />
          </td>
          <td>
            <span>{{
              invoice_product.line_total *
              ((tipscard + tipscash) / invoice_subtotal)
            }}</span>
          </td>
          <td>
            <button
              class="btn btn-warning"
              @click="deleteRow(k, invoice_product)"
            >
              <i class="bx bxs-trash-alt"></i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="total">
      <h3>Total h: {{ invoice_subtotal }}</h3>
    </div>
    <div class="total">
      <h3>Total Tips: {{ tipscash + tipscard }}</h3>
    </div>

    <button type="button" class="btn btn-warning" @click="addNewRow">
      <i class="bx bx-plus-medical"></i>
    </button>

    <div class="input-group mb-3 mt-4">
      <span class="input-group-text">$</span>
      <span class="input-group-text"><h5>Tips Cash</h5></span>
      <input
        type="number"
        class="form-control"
        aria-label="Dollar amount (with dot and two decimal places)"
        v-model.number="tipscash"
      />
    </div>
    <div class="input-group mb-3">
      <span class="input-group-text">$</span>
      <span class="input-group-text"><h5>Tips Card</h5></span>
      <input
        type="text"
        class="form-control"
        aria-label="Dollar amount (with dot and two decimal places)"
        v-model.number="tipscard"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tipscash: 0,
      tipscard: 0,
      invoice_subtotal: 0,
      invoice_total: 0,
      invoice_tax: 5,
      invoice_products: [
        {
          product_no: "",
          product_name: "",
          product_price: "",
          product_qty: "",
          line_total: 0,
        },
      ],
    };
  },

  methods: {
    saveInvoice() {
      console.log(JSON.stringify(this.invoice_products));
    },
    tips() {},
    calculateTotal() {
      var subtotal, total;
      subtotal = this.invoice_products.reduce(function (sum, product) {
        var lineTotal = parseFloat(product.line_total);
        if (!isNaN(lineTotal)) {
          return sum + lineTotal;
        }
      }, 0);

      this.invoice_subtotal = subtotal.toFixed(2);

      total = subtotal * (this.invoice_tax / 100) + subtotal;
      total = parseFloat(total);
      if (!isNaN(total)) {
        this.invoice_total = total.toFixed(2);
      } else {
        this.invoice_total = "0.00";
      }
    },
    calculateLineTotal(invoice_product) {
      var total =
        parseFloat(invoice_product.product_qty) -
        parseFloat(invoice_product.product_price);
      if (!isNaN(total)) {
        invoice_product.line_total = total.toFixed(2);
      }
      this.calculateTotal();
    },
    deleteRow(index, invoice_product) {
      var idx = this.invoice_products.indexOf(invoice_product);
      console.log(idx, index);
      if (idx > -1) {
        this.invoice_products.splice(idx, 1);
      }
      this.calculateTotal();
    },
    addNewRow() {
      this.invoice_products.push({
        product_no: "",
        product_name: "",
        product_price: "",
        product_qty: "",
        line_total: 0,
      });
    },
  },
};
</script>

<style scoped>
.total {
  text-align: right;
  margin-right: 1rem;
}
.container {
  background-color: cornflowerblue;
  margin-bottom: 0%;
  min-height: 800px;
}
</style>
