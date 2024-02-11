<template>
  <div class="editor_panel">
    <h1 @click="togglePanel">Player Details</h1>
    <div v-show="panelVisible">
      <p>mob ID: <input :value="player.mob_id" @input=" ( event ) => handleUpdate(event, 'mob_id', true)" type="number" class="numeric_input"></p>
      <p>Coordinates:
        x: <input :value="player.x" @input=" ( event ) => handleUpdate(event, 'x', true)" type="number" class="numeric_input">
        y: <input :value="player.y" @input=" ( event ) => handleUpdate(event, 'y', true)" type="number" class="numeric_input">
        z: <input :value="player.z" @input=" ( event ) => handleUpdate(event, 'z', true)" type="number" class="numeric_input">
      </p>
      <p>Base Name: <input :value="player.base_name" @input=" ( event ) => handleUpdate(event, 'base_name')"></p>
      <p>Name: <input :value="player.name" @input=" ( event ) => handleUpdate(event, 'name')"></p>
      <p>Alias:
        <GenericArray
          :items="player.alias"
          :new-item="''"
          :renderComponent="renderComponentAlias"
          @change="(value) => handleUpdate({target: {value}}, 'alias')">
        </GenericArray>
      </p>
      <p>Description: <textarea :value="player.description" @input=" ( event ) => handleUpdate(event, 'description')"></textarea></p>
      <p>Lvl: <input :value="player.lvl" @input=" ( event ) => handleUpdate(event, 'lvl', true)" type="number" class="numeric_input"></p>
      <p>exp: <input :value="player.exp" @input=" ( event ) => handleUpdate(event, 'exp', true)" type="number" class="numeric_input"></p>
      <p>Weight: <input :value="player.weight" @input=" ( event ) => handleUpdate(event, 'weight', true)" type="number" class="numeric_input"></p>
      <p>Money: <input :value="player.money" @input=" ( event ) => handleUpdate(event, 'money', true)" type="number" class="numeric_input"></p>
      <p>Race: <select :value="player.race" @input=" ( event ) => handleUpdate(event, 'race')">
          <option value="Orek">Orek</option>
          <option value="Człowiek">Człowiek</option>
          <option value="Szczur">Szczur</option>
      </select></p>
      <p>Proficiency: <select :value="player.proficiency" @input=" ( event ) => handleUpdate(event, 'proficiency')">
          <option value="wojownik">Wojownik</option>
          <option value="kowal">Kowal</option>
          <option value="karczmarz">Karczmarz</option>
          <option value="zielarka">Zielarka</option>
          <option value="strażnik">Strażnik</option>
          <option value="łotrzyk">Łotrzyk</option>
          <option value="gryzoń">Gryzoń</option>
      </select></p>

      <h3>Parametry</h3>
      <p>HP max <input :value="player.params.hp_max" @input=" ( event ) => handleUpdate(event, 'params.hp_max', true)" type="number" class="numeric_input">
      HP <input type="range" min="0" :max="player.params.hp_max" :value="player.params.hp" @input=" ( event ) => handleUpdate(event, 'params.hp', true)">{{ player.params.hp }}</p>
       
      <p>Stamina total <input :value="player.params.stamina_total" @input=" ( event ) => handleUpdate(event, 'params.stamina_total', true)" type="number" class="numeric_input">
      TODO Stamina max <input :value="player.params.stamina_max" @input=" ( event ) => handleUpdate(event, 'params.stamina_max', true)" type="number" class="numeric_input">
      Stamina <input type="range" min="0" :max="player.params.stamina_max" :value="player.params.stamina" @input=" ( event ) => handleUpdate(event, 'params.stamina', true)">{{ player.params.stamina }}</p>
      
      <p>Mana max <input :value="player.params.mana_max" @input=" ( event ) => handleUpdate(event, 'params.mana_max', true)" type="number" class="numeric_input">
      Mana <input type="range" min="0" :max="player.params.mana_max" :value="player.params.mana" @input=" ( event ) => handleUpdate(event, 'params.mana', true)">{{ player.params.mana }}</p>
      
      <p>Satiation max <input :value="player.params.satiation_max" @input=" ( event ) => handleUpdate(event, 'params.satiation_max', true)" type="number" class="numeric_input">
      Satiation <input type="range" min="0" :max="player.params.satiation_max" :value="player.params.satiation" @input=" ( event ) => handleUpdate(event, 'params.satiation', true)">{{ player.params.satiation }}</p>

      <p>Hydration max <input :value="player.params.hydration_max" @input=" ( event ) => handleUpdate(event, 'params.hydration_max', true)" type="number" class="numeric_input">
      Hydration <input type="range" min="0" :max="player.params.hydration_max" :value="player.params.hydration" @input=" ( event ) => handleUpdate(event, 'params.hydration', true)">{{ player.params.hydration }}</p>


      <h3>Stats</h3>
      <p>strength: <input :value="player.stats.strength" @input=" ( event ) => handleUpdate(event, 'stats.strength', true)" type="number" class="numeric_input"></p>
      <p>attack: <input :value="player.stats.attack" @input=" ( event ) => handleUpdate(event, 'stats.attack', true)" type="number" class="numeric_input"></p>
      <p>defence: <input :value="player.stats.defence" @input=" ( event ) => handleUpdate(event, 'stats.defence', true)" type="number" class="numeric_input"></p>
      <p>speed: <input :value="player.stats.speed" @input=" ( event ) => handleUpdate(event, 'stats.speed', true)" type="number" class="numeric_input"></p>
      <p>dexterity: <input :value="player.stats.dexterity" @input=" ( event ) => handleUpdate(event, 'stats.dexterity', true)" type="number" class="numeric_input"></p>
      <p>endurance: <input :value="player.stats.endurance" @input=" ( event ) => handleUpdate(event, 'stats.endurance', true)" type="number" class="numeric_input"></p>

      <h3>Equipment</h3>
      <p>
        <GenericArray
          :items="player.equipment"
          :new-item="{'name':'nazwa', 'description':'desc', 'weight':1}"
          :renderComponent="renderComponentEquipment"
          @change="(value) => handleUpdate({target: {value}}, 'equipment')">
        </GenericArray>
      </p>

      <h3>Slots TODO</h3>
      <p>first hand
        <EquipmentEntry :item="player.slots.first_hand"
        ></EquipmentEntry>
      </p>
      <p>body
        <EquipmentEntry :item="player.slots.body"
        ></EquipmentEntry>
      </p>
      <br>

    </div>
  </div>
</template>

<style>
.numeric_input{
  width: 45px;
}
</style>

<script>
import GenericArray from "./GenericArray.vue";
import AliasEntry from "./AliasEntry.vue";
import EquipmentEntry from "./EquipmentEntry.vue";
//import { toRaw } from 'vue'
import _ from "lodash"

export default {
  components: {
    GenericArray,
    EquipmentEntry
  },
  data() {
    return {
      panelVisible: true
    };
  },
  props: {
    player: Object, // Define time as a prop
    renderComponentAlias: {
      type: Object,
      default: AliasEntry
    },
    renderComponentEquipment: {
      type: Object,
      default: EquipmentEntry
    }
  },
  methods: {
    handleUpdate(event, key, isNumber = false) {
      const record = this.player
      const value = isNumber ? +event.target.value : event.target.value
      _.set(record, key, value)

      this.$emit('change', record)
      //console.log(objekt)
      console.log(this.player)
    },
    togglePanel() {
      this.panelVisible = !this.panelVisible;
    }
  },
  mounted() {
    console.log(this.player)
  }
};
</script>
