<template>
  <button class="btn btn-primary" @click="openModal">
    {{item.name || ">Pusty slot<"}}
  </button>


  <div class="modal fade" ref="itemModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">New message</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form>
            <div class="mb-3">
              <label for="recipient-name" class="col-form-label">Recipient:</label>
              <input
                :value="item.name"
                @input="(event) => handleItemUpdate(event, 'name')"
              />
            </div>
            <div class="mb-3">
              <label for="message-text" class="col-form-label">Message:</label>
              <textarea
                :value="item.description"
                @input="(event) => handleItemUpdate(event, 'description')"
              ></textarea>
            </div>
            <div class="mb-3">
              <label for="recipient-name" class="col-form-label">TODO label weight:</label>
              <input
                :value="item.weight"
                @input="(event) => handleItemUpdate(event, 'weight', true)"
                class="numeric_input"
              />
            </div>

            <div class="mb-3">
              <GenericArray
                :items="Object.entries(item.attr || {}).map( ([key, value]) => ({key, value}))"
                :new-item="{ name: 'nazwa', description: 'desc', weight: 1 }"
                :renderComponent="renderComponentEquipment"
                @change="editItemAttr"
              >
              </GenericArray>
            </div>

          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Send message</button>
        </div>
      </div>
    </div>
  </div>

</template>

<style>
</style>

<script>
//TODO generic dictionary
import { toRaw } from "vue";
import _ from "lodash";
export default {
  data() {
    return {
      modal: null
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
    openModal(){
      this.modal.show()
    },
    editItemAttr(value){
      //TODO
      value.map()
      this.handleUpdate({ target: { value } }, 'equipment')
    }
  },
  mounted() {
    console.log("Benc: ")
    console.log(this.item.name)
    console.log(this.item.attr)
    this.modal = new window.bootstrap.Modal(this.$refs.itemModal)
  },
  unmounted() {
    this.modal.dispose()
  }
};
</script>
