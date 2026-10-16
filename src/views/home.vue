<script setup>
import { reactive, ref } from 'vue'
import DataList from './DataList.vue'

const products = ref([])
const nextProductId = ref(1)
const product = reactive({
  name: '',
  price: '',
  quantity: '',
})

function addProduct() {
  products.value.push({
    id: nextProductId.value++,
    name: product.name.trim(),
    price: Number(product.price),
    quantity: Number(product.quantity),
  })

  product.name = ''
  product.price = ''
  product.quantity = ''
}
</script>

<template>
  <main class="page">
    <header class="page-header">
      <p class="eyebrow">Inventory</p>
      <h1>ادارة المنتجات</h1>
      <p class="intro">Add products and keep track of your current stock.</p>
    </header>

    <section class="panel" aria-labelledby="add-product-title">
      <h2 id="add-product-title">Add a product</h2>
      <form class="product-form" @submit.prevent="addProduct">
        <label>
          Product name
          <input
            v-model="product.name"
            name="name"
            type="text"
            placeholder="e.g. Desk lamp"
            autocomplete="off"
            required
          >
        </label>

        <label>
          Price
          <span class="input-with-prefix">
            <span aria-hidden="true">$</span>
            <input
              v-model="product.price"
              name="price"
              type="number"
              min="0"
              step="0.01"
              placeholder="0.00"
              required
            >
          </span>
        </label>

        <label>
          Quantity
          <input
            v-model="product.quantity"
            name="quantity"
            type="number"
            min="1"
            step="1"
            placeholder="1"
            required
          >
        </label>

        <button type="submit">Add product</button>
      </form>
    </section>

    <DataList :products="products" />
  </main>
</template>

<style scoped>
.page {
  width: min(100% - 2rem, 960px);
  margin: 0 auto;
  padding: 4rem 0;
  color: #17212b;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

.page-header {
  margin-bottom: 2rem;
}

.eyebrow {
  margin: 0 0 0.5rem;
  color: #527c70;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

h1,
h2,
p {
  margin-top: 0;
}

h1 {
  margin-bottom: 0.5rem;
  font-size: clamp(2rem, 5vw, 3rem);
  letter-spacing: -0.04em;
}

.intro {
  margin-bottom: 0;
  color: #63717d;
}

.panel {
  padding: 1.5rem;
  border: 1px solid #e1e8e5;
  border-radius: 1rem;
  background: #fff;
  box-shadow: 0 12px 32px rgb(23 33 43 / 5%);
}

h2 {
  margin-bottom: 1.25rem;
  font-size: 1.125rem;
}

.product-form {
  display: grid;
  grid-template-columns: minmax(180px, 2fr) minmax(120px, 1fr) minmax(110px, 1fr) auto;
  align-items: end;
  gap: 1rem;
}

label {
  display: grid;
  gap: 0.5rem;
  color: #34434e;
  font-size: 0.875rem;
  font-weight: 600;
}

input {
  box-sizing: border-box;
  width: 100%;
  min-width: 0;
  height: 2.75rem;
  padding: 0 0.8rem;
  border: 1px solid #cbd6d2;
  border-radius: 0.5rem;
  background: #fff;
  color: inherit;
  font: inherit;
}

input:focus {
  border-color: #527c70;
  outline: 3px solid rgb(82 124 112 / 16%);
}

.input-with-prefix {
  position: relative;
}

.input-with-prefix > span {
  position: absolute;
  top: 50%;
  left: 0.8rem;
  color: #718078;
  transform: translateY(-50%);
}

.input-with-prefix input {
  padding-left: 1.7rem;
}

button {
  min-height: 2.75rem;
  padding: 0 1rem;
  border: 0;
  border-radius: 0.5rem;
  background: #315f52;
  color: #fff;
  cursor: pointer;
  font: inherit;
  font-weight: 700;
  white-space: nowrap;
}

button:hover {
  background: #244b40;
}

@media (max-width: 720px) {
  .page {
    padding: 2.5rem 0;
  }

  .product-form {
    grid-template-columns: 1fr 1fr;
  }

  .product-form label:first-child,
  .product-form button {
    grid-column: 1 / -1;
  }
}

@media (max-width: 420px) {
  .panel {
    padding: 1rem;
  }

  .product-form {
    grid-template-columns: 1fr;
  }

  .product-form label,
  .product-form button {
    grid-column: 1;
  }
}
</style>