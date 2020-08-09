<template>
    <div class="flowline flex-fill m-1">
        <div class="card text-black bg-white">

          <div class="card-header p-2">
            <span class="align-text-top">{{ title }}</span>
            <b-button type="button" class="close align-top" aria-label="Close" @click="$emit('delete-flowline', title)">
              <span class="align-text-top" aria-hidden="true">&times;</span>
            </b-button>
          </div>

          <draggable class="p-2 list-group kanban-column" :list="arrCards" group="tasks" >
            <Card v-for="element in arrCards" :key="element.name" :cardName="element.name" v-on:delete-card="deleteCard"></Card>
          </draggable>

          <div class="row form-inline p-2">
            <div class="col-10">
              <b-form-input class="w-100" id="inputNewCard" v-model="newCard" required placeholder="Karte hinzufügen..." @keyup.enter="add"></b-form-input>
            </div>
            <div class="col-2">
              <b-button class="float-right" @click="add" variant="success">+</b-button>
            </div>
          </div>

        </div>
      </div>
</template>

<script>
import draggable from "vuedraggable";
import Card from "./Card.vue";
export default {
  name: 'Flowline',
  props: {
    title: String
  },
  components: {
    Card,
    draggable
  },
  data() {
    return {
      newCard: "",
      arrCards: []
    }
  },
  methods: {
    add: function() {
      if (this.newCard) {
        this.arrCards.push({ name: this.newCard });
        this.newCard = "";
      }
    },
    deleteCard: function(cardTitle) {
      this.arrCards = this.arrCards.filter(function(obj) {
        return obj.name !== cardTitle;
      })
    }

  }
}
</script>

<style>
.flowline {
  max-width: 33rem;
}
</style>