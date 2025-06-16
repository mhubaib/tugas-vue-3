<template>
    <div class="miniCart">
        <div class="header">
            <h1>Mini Cart</h1>
            <div class="header-line"></div>
        </div>

        <div class="form">
            <div class="field-form">
                <label for="productName">Nama Produk</label>
                <input id="productName" v-model="productName" type="text" placeholder="Masukkan nama produk..."
                    required />
            </div>

            <div class="field-form">
                <label for="productPrice">Harga Produk</label>
                <input id="productPrice" v-model.number="productPrice" type="number"
                    placeholder="Masukkan harga produk..." required min="1" />
            </div>

            <div class="field-form">
                <label for="productQty">Jumlah Produk</label>
                <input id="productQty" v-model.number="productQty" type="number" placeholder="Masukkan jumlah produk..."
                    required min="1" />
            </div>

            <div class="field-form">
                <label for="productCategories">Kategori Produk</label>
                <input id="productCategories" v-model="productCategories" type="text"
                    placeholder="Masukkan kategori produk..." required />
            </div>

            <div class="button-container">
                <button @click="submitProduct" class="add-button">
                    Add to Cart
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "miniCart",
    data() {
        return {
            productName: "",
            productPrice: 0,
            productQty: 0,
            productCategories: ""
        };
    },
    methods: {
        submitProduct() {
            // Validasi form
            if (!this.productName.trim() || !this.productPrice || !this.productQty || !this.productCategories.trim()) {
                alert("Silahkan lengkapi form!");
                return;
            }
            else {
                const product = {
                    productName: this.productName,
                    productPrice: this.productPrice,
                    productQty: this.productQty,
                    productCategories: this.productCategories
                }
                // Emit produk ke parent
                this.$emit("product-added", product);
            }

            // Reset form
            this.productName = "";
            this.productPrice = 0;
            this.productQty = 0;
            this.productCategories = "";
        }
    }
};
</script>

<style scoped>
.miniCart {
    background: #ffffff;
    border: 1px solid #e5e7eb;
    border-radius: 12px;
    padding: 24px;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    min-width: 400px;
}

.header {
    text-align: center;
    margin-bottom: 24px;
}

.header h1 {
    color: #1f2937;
    font-size: 24px;
    font-weight: 600;
    margin: 0 0 8px 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.header-line {
    width: 40px;
    height: 2px;
    background: #3b82f6;
    margin: 0 auto;
}

.form {
    width: 100%;
}

.field-form {
    margin-bottom: 20px;
    margin-right: 16px;
}

.field-form label {
    display: block;
    color: #374151;
    font-size: 14px;
    font-weight: 500;
    margin-bottom: 6px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.field-form input {
    width: 100%;
    padding: 12px 8px;
    margin-right: 16px;
    background: #ffffff;
    border: 1px solid #d1d5db;
    border-radius: 8px;
    font-size: 14px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    transition: all 0.2s ease;
    color: #1f2937;
}

.field-form input:focus {
    outline: none;
    border-color: #3b82f6;
    box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.field-form input::placeholder {
    color: #9ca3af;
}

.button-container {
    margin-top: 24px;
}

.add-button {
    width: 100%;
    background: #1f2937;
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 500;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    cursor: pointer;
    transition: all 0.2s ease;
}

.add-button:hover {
    background: #374151;
    transform: translateY(-1px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.add-button:active {
    transform: translateY(0);
}

/* Responsive design */
@media (max-width: 480px) {
    .miniCart {
        padding: 20px;
        max-width: 100%;
    }

    .header h1 {
        font-size: 20px;
    }

    .field-form input {
        padding: 10px 14px;
    }

    .add-button {
        padding: 10px 20px;
    }
}
</style>