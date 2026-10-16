<script setup>
defineProps({
  products: {
    type: Array,
    required: true,
  },
})
</script>

<template>
  <section class="product-list" aria-labelledby="product-list-title">
    <div class="list-heading">
      <div>
        <p class="eyebrow">Your inventory</p>
        <h2 id="product-list-title">Products</h2>
      </div>
      <span class="count">{{ products.length }} {{ products.length === 1 ? 'item' : 'items' }}</span>
    </div>

    <p v-if="products.length === 0" class="empty-state">
      No products yet. Use the form above to add your first product.
    </p>

    <div v-else class="table-wrap">
      <table>
        <thead>
          <tr>
            <th scope="col">Product</th>
            <th scope="col">Price</th>
            <th scope="col">Quantity</th>
            <th scope="col">Total value</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.id">
            <th scope="row">{{ product.name }}</th>
            <td>{{ product.price.toLocaleString(undefined, { style: 'currency', currency: 'USD' }) }}</td>
            <td>{{ product.quantity }}</td>
            <td>{{ (product.price * product.quantity).toLocaleString(undefined, { style: 'currency', currency: 'USD' }) }}</td>
          </tr>
        </tbody>
      </table>
      <p class="total-value">
        Total value: {{ products.reduce((total, product) => total + product.price * product.quantity, 0).toLocaleString(undefined, { style: 'currency', currency: 'USD' }) }}
      </p>
    </div>
  </section>
</template>

<style scoped>
.product-list {
  margin-top: 2rem;
  padding: 1.5rem;
  border: 1px solid #e1e8e5;
  border-radius: 1rem;
  background: #fff;
  box-shadow: 0 12px 32px rgb(23 33 43 / 5%);
}

.list-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 1.25rem;
}

.eyebrow {
  margin: 0 0 0.35rem;
  color: #527c70;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

h2 {
  margin: 0;
  color: #17212b;
  font-size: 1.125rem;
}

.count {
  padding: 0.35rem 0.65rem;
  border-radius: 999px;
  background: #edf4f1;
  color: #315f52;
  font-size: 0.8rem;
  font-weight: 700;
  white-space: nowrap;
}

.total-value {
  margin: 1rem 0 0;
  padding: 0.75rem 0;
  border-top: 1px solid #edf0ef;
  color: #17212b;
  font-weight: 700;
}

.empty-state {
  margin: 0;
  padding: 1.5rem 1rem;
  border: 1px dashed #cbd6d2;
  border-radius: 0.65rem;
  color: #63717d;
  text-align: center;
}

.table-wrap {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

th,
td {
  padding: 0.9rem 0.75rem;
  border-bottom: 1px solid #edf0ef;
  color: #34434e;
  font-size: 0.9rem;
}

thead th {
  color: #718078;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

tbody th {
  color: #17212b;
  font-weight: 600;
}

tbody tr:last-child th,
tbody tr:last-child td {
  border-bottom: 0;
}

@media (max-width: 520px) {
  .product-list {
    padding: 1rem;
  }

  th,
  td {
    padding: 0.75rem 0.5rem;
    font-size: 0.8rem;
  }
}
</style>
