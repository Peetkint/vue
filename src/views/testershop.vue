<template>
  <div class="outer-container">
    <div class="container">
      <h1>ร้านขายของออนไลน์</h1>
      <div class="product-list">
        <div v-for="product in products" :key="product.id" class="product-card">
            <center>
            <v-card width="150" height="150px" class="product-card" >
                <v-img :src="product.imageUrl" alt="Product Image" >
                </v-img>
            </v-card></center>
          <h2>{{ product.product_name }}</h2>
          <p>ราคา: {{ product.price }} บาท</p>
          <p>จำนวน: {{ product.amount }}</p>
          <div class="quantity-container">
            <input v-model.number="product.quantityToAdd" type="number" min="1" :max="product.amount" class="quantity-input" />
            <button @click="addToCart(product)" class="btn">เพิ่มใส่ตะกร้า</button>
          </div>
        </div>
      </div>
      <div class="cart">
        <h2><v-icon>mdi-cart</v-icon>ตะกร้าสินค้า</h2>
        <div v-for="(item, index) in cart" :key="index" class="cart-item">
            <br/>
          <p><strong>สินค้า</strong>   &nbsp;&nbsp;: &nbsp; &nbsp; &nbsp;{{ item.product_name }}</p>
          <p><strong>ราคา</strong>   &nbsp;&nbsp;: &nbsp; &nbsp; &nbsp;{{ item.price }} บาท</p>
          <p><strong>จำนวน</strong> : &nbsp; &nbsp; &nbsp;({{ item.quantity }} ชิ้น)</p>
          <br/>
          <p><strong>รวม</strong> &nbsp;&nbsp;&nbsp;&nbsp;: &nbsp; &nbsp; &nbsp;{{ item.quantity*item.price}} บาท</p>
          <br/>
          <div class="quantity-container">
            <button @click="updateQuantity(item, 'reduce')" class="btn">-</button>
            <input type="text" :value="item.quantity" class="quantity-display" readonly />
            <button @click="updateQuantity(item, 'increase')" class="btn">+</button>
            
            <button @click="removeFromCart(item.product_name)" class="btn" style="margin-left: auto;">ลบสินค้า</button>
          </div>
        </div>
        <p v-if="cart.length === 0">ตะกร้าสินค้าว่างเปล่า</p>
        <p class="total">รวมทั้งหมด: {{ total }} บาท</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        const response = await this.axios.get('http://localhost:3000/admin');
        this.products = response.data.map(product => ({
          ...product,
          quantityToAdd: 1 // เพิ่ม property quantityToAdd ให้กับสินค้า
        }));
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    addToCart(product) {
      const existingItem = this.cart.find(item => item.product_name === product.product_name);
      const quantityToAdd = parseInt(product.quantityToAdd);

      if (existingItem) {
        const totalQuantity = existingItem.quantity + quantityToAdd;
        if (totalQuantity > product.amount) {
          alert('ไม่สามารถเพิ่มสินค้าเกินจำนวนที่มีอยู่ได้');
          return;
        }
        existingItem.quantity += quantityToAdd;
      } else {
        if (quantityToAdd > product.amount) {
          alert('ไม่สามารถเพิ่มสินค้าเกินจำนวนที่มีอยู่ได้');
          return;
        }
        this.cart.push({
          ...product,
          quantity: quantityToAdd
        });
      }

      // ลดจำนวนสินค้าในสต็อก
      const productIndex = this.products.findIndex(prod => prod.product_name === product.product_name);
      if (productIndex !== -1) {
        this.products[productIndex].amount -= quantityToAdd;
      }

      product.quantityToAdd = 1; // Reset the quantityToAdd property
    },
    updateQuantity(item, action) {
      const productIndex = this.products.findIndex(prod => prod.product_name === item.product_name);
      if (productIndex === -1) return;

      if (action === 'reduce') {
        if (item.quantity === 1) return;

        item.quantity -= 1;

        // เพิ่มจำนวนสินค้าในสต็อก
        this.products[productIndex].amount += 1;

        if (item.quantity === 0) {
          this.cart = this.cart.filter(cartItem => cartItem.product_name !== item.product_name);
        }
      } else if (action === 'increase') {
        // ตรวจสอบว่าสินค้าที่เพิ่มมีในสต็อกเพียงพอหรือไม่
        if (this.products[productIndex].amount === 0) {
          alert('สินค้าในสต็อกไม่เพียงพอ');
          return;
        }

        item.quantity += 1;

        // ลดจำนวนสินค้าในสต็อก
        this.products[productIndex].amount -= 1;
      }
    },
    removeFromCart(product_name) {
      const itemIndex = this.cart.findIndex(item => item.product_name === product_name);
      if (itemIndex !== -1) {
        // เพิ่มจำนวนสินค้าในสต็อก
        const productIndex = this.products.findIndex(prod => prod.product_name === product_name);
        if (productIndex !== -1) {
          this.products[productIndex].amount += this.cart[itemIndex].quantity;
        }

        // ลบสินค้าออกจากตะกร้า
        this.cart.splice(itemIndex, 1);
      }
    }
  }
};
</script>

<style scoped>
.outer-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f9f9f9;
  flex-direction: column;
}

.container {
  max-width: 1000px;
  margin: 20px;
  padding: 20px;
  text-align: center;
  font-family: Arial, sans-serif;
  background-color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

h1 {
  color: #4CAF50;
  margin-bottom: 20px;
}

.product-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.product-card {
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: 20px;
  padding: 20px;
  width: calc(33.333% - 40px);
  box-sizing: border-box;
  transition: transform 0.2s, box-shadow 0.2s;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.product-card h2 {
  color: #333;
  margin-bottom: 10px;
  font-size: 20px;
}

.product-card p {
  color: #777;
  font-size: 16px;
  margin: 5px 0;
}

.btn {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn:hover {
  background-color: #45a049;
}

.cart {
   margin-top: 20px;
  text-align: left;
  border: 1px solid #ddd; /* เส้นขอบทั้ง 4 ด้าน ความหนา 1px สีเทาอ่อน */
  padding: 10px; /* ใส่ padding เพื่อให้เนื้อที่ส่วนในของ .cart ไม่ติดกับขอบ */
  border-radius: 8px;
}

.cart h2 {
  font-size: 24px;
  color: #333;
}

.cart-item {
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
}

.total {
  font-size: 20px;
  font-weight: bold;
  margin-top: 20px;
}

.quantity-container {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.quantity-input {
  width: 50px;
  margin-right: 10px;
  text-align: center;
}

.quantity-display {
  width: 50px;
  text-align: center;
  border: 1px solid #ddd;
  margin: 0 10px;
  padding: 5px;
}
</style>
