<template>
  <div class="product p-4">
    <div class="product-image">
      <img :src="data.photo" :alt="data.item_name" />
    </div>
    <div class="product-description">
      <span class="h1 text-bold">{{ data.item_name }}</span>
      <div>
        {{ data.item_description }}
      </div>
    </div>
    <hr class="w-100" />
    <div class="product-price">
      <b-form-group>
        <div
          v-for="price in data.prices"
          :key="price.size_id"
          class="d-flex justify-content-between align-items-end"
        >
          <b-form-radio name="choose-size" size="lg">{{
            price.size
          }}</b-form-radio>
          <span> {{ price.formatted_price }}</span>
        </div>
      </b-form-group>
    </div>
    <hr class="w-100" />
    <div class="product-nutritional">
      <div class="font-weight-bold mb-2">
        Пищевая ценность на 100г. продукта
      </div>
      <div class="d-flex justify-content-between">
        <div class="nutritional-item text-center">
          <div>
            Белки
          </div>
          <span>{{ data.item_protein }}</span>
        </div>
        <div class="nutritional-item text-center">
          <div>
            Жиры
          </div>
          <span>{{ data.item_fats }}</span>
        </div>
        <div class="nutritional-item text-center">
          <div>
            Углеводы
          </div>
          <span>{{ data.item_carbohydrates }}</span>
        </div>
        <div class="nutritional-item text-center">
          <div>
            Калории
          </div>
          <span>{{ data.item_calories }}</span>
        </div>
      </div>
    </div>
    <hr class="w-100" />
    <div class="product-dough">
      <div class="font-weight-bold mb-2">Выберите тесто</div>
      <b-form-group>
        <div
          v-for="dough in doughTypes.sub_item"
          :key="dough.sub_item_id"
          class="d-flex justify-content-start align-items-end"
        >
          <b-form-radio name="choose-dough">{{
            dough.sub_item_name
          }}</b-form-radio>
          <span class="ml-2"> + {{ dough.price }} Р</span>
        </div>
      </b-form-group>
    </div>
    <hr class="w-100" />
    <div class="product-additional">
      <div class="font-weight-bold mb-2">Добавки к пицце</div>
      <div
        v-for="item in additionalIngridients.sub_item"
        :key="item.sub_item_id"
        class="d-flex justify-content-start align-items-end"
      >
        <span>{{ item.sub_item_name }}</span>
        <span class="ml-2"> + {{ item.price }} Р</span>
      </div>
    </div>
  </div>
</template>

<script>
const DOUGH_ID = 5;
const ADDITIONAL_ID = 1;
export default {
  props: {
    data: Object
  },
  computed: {
    doughTypes() {
      return this.data.addon_item.filter(obj => obj.subcat_id == DOUGH_ID)[0];
    },
    additionalIngridients() {
      return this.data.addon_item.filter(
        obj => obj.subcat_id == ADDITIONAL_ID
      )[0];
    }
  }
};
</script>

<style lang="scss">
.product {
  border: 1px solid #cecece;
  border-radius: 5px;
  background-color: #fff;
}
</style>
