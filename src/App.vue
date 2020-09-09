<template>
  <div id="app">
    <div class="container py-3">
      <div v-if="isError" class="text-center">
        Error loading data
      </div>
      <div v-else class="d-flex justify-content-center align-items-center">
        <div v-if="isLoading" class="loading-spinner">
          <b-spinner type="grow" label="Spinning"></b-spinner>
        </div>
        <product-component v-else :data="data" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductComponent from "./components/ProductComponent.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    ProductComponent
  },
  data() {
    return {
      data: Object,
      isLoading: true,
      isError: false
    };
  },
  mounted() {
    axios
      .get(
        "https://vsem-edu-oblako.ru/singlemerchant/api/loadItemDetails?merchant_keys=929990d3b27944af404a5eb3ee1ec4f6&device_id=89000001020&lang=ru&device_platform=mobile&json=true&item_id=18094140#get"
      )
      .then(response => {
        this.data = response.data.details.data;
        this.isLoading = false;
      })
      .catch(() => {
        this.isError = true;
      });
  }
};
</script>

<style lang="scss">
html,
body {
  height: 100%;
}
body {
  background-color: #ececec !important;
}
img {
  width: 100%;
}
.loading-spinner {
  position: absolute;
  top: 50%;
}
</style>
