<template>
  <button class="btn btn-primary" @click="cardVisible = !cardVisible">
    {{item.name || ">Pusty slot<"}}
  </button>
  <div class="card item_card" style="width: 18rem" v-show="cardVisible">
    <div class="card-body">
      <h5 class="card-title">{{ item.name }}</h5>
      <button
        class="btn btn-close"
        @click="cardVisible = !cardVisible"
      ></button>
      <p class="card-text">{{ item.description }}</p>
      <a href="#" class="btn btn-primary">Go somewhere</a>
      <input
        :value="item.name"
        @input="(event) => handleItemUpdate(event, 'name')"
      />
      <textarea
        :value="item.description"
        @input="(event) => handleItemUpdate(event, 'description')"
      ></textarea>
      <input
        :value="item.weight"
        @input="(event) => handleItemUpdate(event, 'weight', true)"
        class="numeric_input"
      />
    </div>
  </div>
</template>

<style>
.item_card {
  position: fixed;
  top: 100px;
  left: 200px;
  box-shadow: 0px 0px 15px 1000000px rgba(0, 0, 0, 0.5);
}
</style>

<script>
import { toRaw } from "vue";
import _ from "lodash";
export default {
  data() {
    return {
      cardVisible: false,
    };
  },
  props: {
    item: Object,
  },
  methods: {
    handleItemUpdate(event, key, isNumber = false) {
      const record = structuredClone(toRaw(this.item));
      const value = isNumber ? +event.target.value : event.target.value;
      _.set(record, key, value);

      this.$emit("change", record);
    },
  },
  mounted() {
    console.log(this.item);
  },
};
</script>
