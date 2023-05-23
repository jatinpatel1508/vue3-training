<script>
// import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
import RoomDemo from "./components/RoomDemo.vue";
import ApiDemo from "./components/ApiDemo.vue";

export default {
  name: "App",
  components: { RoomDemo, ApiDemo },
  props: {},
  data() {
    return {
      isInvoiceDemo: false,
      isRoomDemo: false,
      isAPIDemo: false,
      isDisplayInvoiceJson: 0,
      categories: [
        {
          name: "1",
          display: "Category 1",
        },
        {
          name: "2",
          display: "Category 2",
        },
        {
          name: "3",
          display: "Category 3",
        },
      ],
      selectedCategory: 1,
      invProducts: [
        /*{
          product_name: "test1",
          category: "1",
          price: 100,
          discount: 5,
          total: 95,
        },*/
      ],
      invProdForDisplay: [],
    };
  },
  methods: {
    addProducts() {
      const tempProduct = {
        product_name: "",
        category: "",
        price: null,
        discount: null,
        total: null,
      };
      this.invProducts.push(tempProduct);
    },
    removeProduct(index) {
      this.invProducts.splice(index, 1);
    },
    generateTable() {
      let tempInvProd = this.invProducts.map((invProd) => {
        let catDetail = this.categories.filter((cat) => {
          return cat.name == invProd.category;
        });
        console.log(catDetail);
        invProd.category = catDetail[0].display;
        return invProd;
      });

      this.invProdForDisplay = tempInvProd;
    },
    calculateDiscount(product) {
      console.log(product);
      product.total = product.price;
      if (product.discount != null) {
        let discount = (product.price * product.discount) / 100;
        product.total = product.price - discount;
      }
    },
  },
  beforeCreate() {
    console.log("beforeCreate() from parent...");
  },
  created() {
    console.log("created() from parent...");
  },
  beforeMount() {
    console.log("beforeMount() from parent...");
  },
  mounted() {
    console.log("mounted() from parent...");
  },
  beforeUpdate() {
    console.log("beforeUpdate() from parent...");
  },
  updated() {
    console.log("updated() from parent...");
  },
  beforeUnmount() {
    console.log("beforeUnmount() from parent...");
  },
  unmounted(){
    console.log("unmounted() from parent...");
  }
};
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/logo.svg"
      width="125"
      height="125"
    />
    <div class="vue-demo">
      <button @click="this.isInvoiceDemo = this.isInvoiceDemo == 1 ? 0 : 1">
        <span v-if="this.isInvoiceDemo == 1">Hide</span
        ><span v-else>Show</span> Invoice Demo
      </button>
      <button @click="this.isRoomDemo = this.isRoomDemo == 1 ? 0 : 1">
        <span v-if="this.isRoomDemo == 1">Hide</span
        ><span v-else>Show</span> Room Demo
      </button>
      <button @click="this.isAPIDemo = this.isAPIDemo == 1 ? 0 : 1">
        <span v-if="this.isAPIDemo == 1">Hide</span><span v-else>Show</span> API
        Demo
      </button>
    </div>

    <!-- INVOICE DEMO CODE START -->
    <div class="invoice-wrapper" v-show="isInvoiceDemo">
      <!-- <HelloWorld msg="You did it!" /> -->
      <div class="invoice-head">
        <div class="add-more">
          <button @click="addProducts()">Add Product</button>
        </div>
        <div
          class="inv-prod"
          v-for="(product, index) of invProducts"
          :key="index"
        >
          <div class="product-name inv-pading inv-border">
            <input type="text" v-model="product.product_name" />
          </div>
          <div class="product-category inv-pading inv-border">
            <select v-model="product.category">
              <option
                v-for="(category, index) in categories"
                :key="index"
                :value="category.name"
              >
                {{ category.display }}
              </option>
            </select>
          </div>
          <div class="product-price inv-pading inv-border">
            <input
              type="number"
              v-model="product.price"
              @keyup="calculateDiscount(product)"
            />
          </div>
          <div class="product-discount inv-pading inv-border">
            <input
              type="number"
              v-model="product.discount"
              @keyup="calculateDiscount(product)"
            />
          </div>
          <div class="product-total inv-pading inv-border">
            <input type="number" v-model="product.total" />
          </div>
          <div class="remove-product inv-pading inv-border" style="width: 32px">
            <div>
              <button @click="removeProduct(index)" style="font-weight: bold">
                -
              </button>
            </div>
          </div>
        </div>
        <div class="generate">
          <button @click="generateTable()">Generate Table</button>
        </div>
      </div>

      <div class="invoice-table">
        <div class="inv-prod-head">
          <div class="tbl-prod-name-head inv-head-pading">Product Name</div>
          <div class="tbl-prod-category-head inv-head-pading">
            Product Category
          </div>
          <div class="tbl-prod-price-head inv-head-pading">Product Price</div>
          <div class="tbl-prod-disc-head inv-head-pading">
            Product Discount (%)
          </div>
          <div class="tbl-prod-total-head inv-head-pading">Product Total</div>
        </div>
        <div
          class="inv-prod-detail"
          v-for="(prod, index) in invProdForDisplay"
          :key="index"
        >
          <div class="tbl-prod-name inv-prod-detail-pading">
            {{ prod.product_name }}
          </div>
          <div class="tbl-prod-category inv-prod-detail-pading">
            {{ prod.category }}
          </div>
          <div class="tbl-prod-price inv-prod-detail-pading">
            {{ prod.price }}
          </div>
          <div class="tbl-prod-disc inv-prod-detail-pading">
            {{ prod.discount }}
          </div>
          <div class="tbl-prod-total inv-prod-detail-pading">
            {{ prod.total }}
          </div>
        </div>
      </div>

      <button class="show-room-json" @click="isDisplayInvoiceJson = 1">
        Display Invoice JSON
      </button>
      <pre v-show="isDisplayInvoiceJson">{{ invProducts }}</pre>
    </div>

    <!-- ROOM DEMO CODE START -->
    <div v-show="isRoomDemo">
      <room-demo />
    </div>

    <div v-if="isAPIDemo">
      <api-demo />
    </div>
  </header>

  <!-- <RouterView /> -->
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.invoice-wrapper {
  border: 1px solid;
  padding: 15px;
}
.inv-prod {
  display: flex;
}

.inv-pading {
  padding: 10px;
}
.inv-border {
  border: 1px solid #ccc;
}
.inv-prod-head {
  display: flex;
}
.inv-head-pading {
  padding: 10px;
  /* font-weight: bold; */
  border: 1px solid #ccc;
}
.inv-prod-detail {
  display: flex;
}
.inv-prod-detail-pading {
  padding: 10px;
  width: 6rem;
  text-align: center;
  border: 1px solid #ccc;
}
</style>
