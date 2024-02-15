<template>
  <div>
    <span v-for="item, index in aviableItems" :key="index">{{ item.name }}</span>
    <EquipmentEntry :item="currentItem"/>
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
import EquipmentEntry from "./EquipmentEntry.vue";
export default {
    data() {
        return {
            cardVisible: false,
        };
    },
    props: {
        currentItem: Object,
        aviableItems: Array
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
    components: { EquipmentEntry }
};
</script>
