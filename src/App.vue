<template>
  <div id="app">
    <div class="app-container">
      <miniCart @product-added="addProduct" />

      <div v-if="cart.length" class="cart-display">
        <div class="table-header">
          <h2>Shopping Cart</h2>
          <div class="cart-count">{{ cart.length }} item{{ cart.length > 1 ? 's' : '' }}</div>
        </div>

        <div class="table-container">
          <table class="cart-table">
            <thead>
              <tr>
                <th>Nama</th>
                <th>Harga</th>
                <th>Jumlah</th>
                <th>Kategori</th>
                <th>Subtotal</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(product, index) in cart" :key="index" class="cart-item">
                <td class="product-name">{{ product.productName }}</td>
                <td class="price">Rp{{ formatPrice(product.productPrice) }}</td>
                <td class="quantity">{{ product.productQty }}</td>
                <td class="category">
                  <span class="category-tag">{{ product.productCategories }}</span>
                </td>
                <td class="subtotal">Rp{{ formatPrice(product.productPrice * product.productQty) }}</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="total-section">
          <div class="total-container">
            <span class="total-label">Total Pembayaran</span>
            <span class="total-amount">Rp{{ formatPrice(totalPrice) }}</span>
          </div>
        </div>
      </div>

      <div v-else class="empty-cart">
        <div class="empty-icon">📦</div>
        <h3>Keranjang Kosong</h3>
        <p>Belum ada produk yang ditambahkan</p>
      </div>
    </div>
  </div>
</template>

<script>
import miniCart from './components/miniCart.vue';

export default {
  name: 'App',
  components: {
    miniCart
  },
  data() {
    return {
      cart: []
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((sum, item) => {
        return sum + item.productPrice * item.productQty;
      }, 0);
    }
  },
  created() {
    // Load initial cart data if needed
    alert('Selamat datang di aplikasi keranjang belanja!');
  },
  methods: {
    addProduct(product) {
      this.cart.push(product);
    },
    formatPrice(price) {
      return new Intl.NumberFormat('id-ID').format(price);
    }
  }
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  min-height: 100vh;
  background: #f8fafc;
  padding: 32px 20px;
}

.app-container {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: start;
}

.cart-display {
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.table-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  padding-bottom: 16px;
  border-bottom: 1px solid #e5e7eb;
}

.table-header h2 {
  margin: 0;
  color: #1f2937;
  font-size: 20px;
  font-weight: 600;
}

.cart-count {
  background: #6b7280;
  color: white;
  padding: 4px 12px;
  border-radius: 16px;
  font-size: 13px;
  font-weight: 500;
}

.table-container {
  overflow-x: auto;
  margin-bottom: 20px;
}

.cart-table {
  width: 100%;
  border-collapse: collapse;
  border-radius: 8px;
  overflow: hidden;
  border: 1px solid #e5e7eb;
}

.cart-table thead th {
  background: #1f2937;
  color: white;
  padding: 12px;
  text-align: left;
  font-weight: 500;
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.cart-item {
  background: white;
  transition: background-color 0.2s ease;
}

.cart-item:hover {
  background: #f9fafb;
}

.cart-item:not(:last-child) {
  border-bottom: 1px solid #f3f4f6;
}

.cart-table td {
  padding: 12px;
  font-size: 14px;
  color: #374151;
}

.product-name {
  font-weight: 500;
  color: #1f2937;
}

.price,
.subtotal {
  font-weight: 500;
  color: #3b82f6;
}

.quantity {
  text-align: center;
  font-weight: 500;
}

.category-tag {
  background: #6b7280;
  color: white;
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: 500;
  display: inline-block;
}

.total-section {
  border-top: 1px solid #e5e7eb;
  padding-top: 16px;
}

.total-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9fafb;
  padding: 16px 20px;
  border-radius: 8px;
  border: 1px solid #e5e7eb;
}

.total-label {
  font-size: 16px;
  font-weight: 500;
  color: #374151;
}

.total-amount {
  font-size: 18px;
  font-weight: 600;
  color: #1f2937;
}

.empty-cart {
  text-align: center;
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 48px 32px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.empty-icon {
  font-size: 48px;
  margin-bottom: 16px;
  opacity: 0.6;
}

.empty-cart h3 {
  font-size: 18px;
  font-weight: 600;
  color: #1f2937;
  margin: 0 0 8px 0;
}

.empty-cart p {
  color: #6b7280;
  font-size: 14px;
  margin: 0;
}

/* Responsive design */
@media (max-width: 768px) {
  .app-container {
    grid-template-columns: 1fr;
    gap: 24px;
  }

  .cart-display {
    padding: 20px;
  }

  .table-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }

  .cart-table {
    font-size: 13px;
  }

  .cart-table th,
  .cart-table td {
    padding: 10px 8px;
  }

  .total-container {
    flex-direction: column;
    gap: 8px;
    text-align: center;
  }

  .empty-cart {
    padding: 32px 20px;
  }
}

@media (max-width: 480px) {
  #app {
    padding: 20px 16px;
  }

  .cart-table {
    font-size: 12px;
  }

  .cart-table th,
  .cart-table td {
    padding: 8px 6px;
  }

  .category-tag {
    font-size: 11px;
    padding: 3px 6px;
  }

  .empty-icon {
    font-size: 36px;
  }
}
</style>