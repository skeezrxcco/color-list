<template>
  <!-- This example requires Tailwind CSS v2.0+ -->
  <div class="bg-white">
    <div class="max-w-7xl mx-auto py-24 px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:flex-col sm:align-center">
        <h1 class="text-5xl font-extrabold text-gray-900 sm:text-center">Color Lists 👨🏻‍🎨</h1>
        <p class="mt-5 text-xl text-gray-500 sm:text-center">Add colors and make them slide between the 2 lists</p>
      </div>
      <div
        class="mt-12 space-y-4 sm:mt-16 sm:space-y-0 sm:grid sm:grid-cols-2 sm:gap-10 lg:max-w-4xl lg:mx-auto xl:max-w-3xl xl:mx-auto  xl:grid-cols-2  h-96">
        <!-- List 1 -->
        <div @dragover.prevent @dragenter.prevent @drop="onDrop($event, 1)"
          class="border border-gray-200 rounded-lg shadow-sm divide-y divide-gray-200">
          <!-- List Header -->
          <ListHeader :currentList="1" :listFull="listOneFull" :listTargetFull="listTwoFull"
            :selectedCard="selectedCard" @addCard="addCard" @removeCard="removeCard" :item="selectedObj" />

          <!-- Card -->
          <div v-for="item in listOne" :key="item.title" draggable @dragstart="startDrag($event, item)"
            class="col-span-1 flex shadow-sm rounded-md mb-2" :class="[isDragging ? 'cursor-move	' : 'cursor-pointer']"
            :style="selectedCard == item.id ? 'border: 1px solid yellow;' : ''">
            <div class="flex-shrink-0 flex items-center justify-center w-16 text-white text-sm font-medium rounded-l-md"
              @click="selectCard(item)" :style="{ 'background-color': item.color.hex }"></div>
            <div
              class="card-select flex-1 flex items-center justify-between border-t border-r border-b border-gray-200 bg-white rounded-r-md">
              <div class=" relative flex-1 px-4 py-2 text-base">
                <v-select v-model="item.color.name" :options="colorOptions" label="name"
                  @input="setColor($event, item)">
                </v-select>
              </div>

              <!-- DropDown Menu -->
              <DropDownMenu :item="item" :isToggleMenu="item.toggleMenu" :listFull="listOneFull"
                :listTargetFull="listTwoFull" :currentList="1" @copyCard="copyCard" @removeCard="removeCard"
                @toggleMenu="toggleMenu" @move="move" @reference="reference" />

            </div>

          </div>
        </div>

        <!-- List 2 -->
        <div @dragover.prevent @dragenter.prevent @drop="onDrop($event, 2)"
          class="border border-gray-200 rounded-lg shadow-sm divide-y divide-gray-200">
          <!-- List Header -->
          <ListHeader :currentList="2" :listFull="listTwoFull" :listTargetFull="listOneFull"
            :selectedCard="selectedCard" @addCard="addCard" @removeCard="removeCard" :item="selectedObj" />
          <!-- Card -->
          <div v-for="item in listTwo" :key="item.title" draggable @dragstart="startDrag($event, item)"
            class="col-span-1 flex shadow-sm rounded-md mb-2" :class="[isDragging ? 'cursor-move	' : 'cursor-pointer']"
            :style="selectedCard == item.id ? 'border: 1px solid yellow;' : ''">
            <div class="flex-shrink-0 flex items-center justify-center w-16 text-white text-sm font-medium rounded-l-md"
              @click="selectCard(item)" :style="{ 'background-color': item.color.hex }"></div>
            <div
              class="card-select flex-1 flex items-center justify-between border-t border-r border-b border-gray-200 bg-white rounded-r-md">
              <div class=" relative flex-1 px-4 py-2 text-base">
                <v-select v-model="item.color.name" :options="colorOptions" label="name"
                  @input="setColor($event, item)">
                </v-select>
              </div>
              <div class="flex-shrink-0 pr-2">
                <!-- DropDown Menu -->
                <DropDownMenu :item="item" :isToggleMenu="item.toggleMenu" :listFull="listTwoFull"
                  :listTargetFull="listOneFull" :currentList="2" @copyCard="copyCard" @removeCard="removeCard"
                  @toggleMenu="toggleMenu" @move="move" @reference="reference" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

import ListHeader from './components/List/ListHeader.vue'
import DropDownMenu from './components/List/ListItem/DropDownMenu.vue'
import colorsOptions from './data/colors.js'
export default {

  components: {
    DropDownMenu,
    ListHeader,
  },
  data() {
    return {
      idCounter: 0,
      items: [],
      colorOptions: colorsOptions,
      listOneFull: false,
      listTwoFull: false,
      referenceMessage: false,
      isDragging: false,
      targetList: "",
      selectedCard: null,
      selectedObj: { listId: null },
    }
  },
  computed: {
    listOne() {
      return this.items.filter(item => item.listId === 1)
    },
    listTwo() {
      return this.items.filter(item => item.listId === 2)
    },
  },
  methods: {
    // DRAG & DROP 🖱
    onDrop(evt, listId) {
      let droppedList = [];
      listId === 1 ? droppedList = this.listOneFull : droppedList = this.listTwoFull;

      // If the list is full we exit the function
      if (droppedList) {
        return false;
      }

      const itemID = evt.dataTransfer.getData('itemID')
      const item = this.items.find(item => item.id == itemID)
      item.listId = listId
      this.isDragging = false;

      this.refreshLists();
    },
    startDrag(evt, item) {
      this.isDragging = true;
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
      this.items.toggleMenu = false;
    },

    // BREAD 🍞 
    addCard(listId) {
      this.idCounter++;
      const newCard = {
        id: this.idCounter,
        color: {
          name: "",
          hex: "#808080",
        },
        listId: listId,
        toggleMenu: false,
      };
      this.items.push(newCard);
      this.refreshLists();

    },
    setColor(e, item) {
      let itemIndex = this.items.findIndex((objItem => objItem.id == item.id));
      this.items[itemIndex].color.name = e.name
      this.items[itemIndex].color.hex = e.hex
    },
    removeCard(item) {
      let itemIndex = this.items.findIndex((objItem => objItem.id == item.id));
      if (itemIndex > -1) {
        this.items.splice(itemIndex, 1);
      }
      this.selectedCard = null;
      this.refreshLists();
    },

    // CHECKS & VALIDATIONS 🥅
    refreshLists() {
      if (this.listOne.length >= 6) {
        this.listOneFull = true
      } else {
        this.listOneFull = false
      }
      if (this.listTwo.length >= 6) {
        this.listTwoFull = true
      } else {
        this.listTwoFull = false
      }
      this.closeMenus();
      this.selectedCard = null
    },

    // UTILITY 🛠 
    copyCard(item, isFull, listId) {
      console.log([item, isFull, listId]);
      // If the list is full we exit the function
      if (isFull) {
        return false;
      }
      this.idCounter++;
      const newCard = {
        id: this.idCounter,
        color: {
          name: item.color.name,
          hex: item.color.hex,
        },
        listId: listId,
        toggleMenu: false,
      };
      this.items.push(newCard);

      // We refresh the list 
      this.refreshLists();
    },
    move(item) {
      let itemIndex = this.items.findIndex((objItem => objItem.id == item.id));
      this.items[itemIndex].listId === 1 ? this.items[itemIndex].listId = 2 : this.items[itemIndex].listId = 1;
      this.items[itemIndex].toggleMenu = false;
      this.refreshLists();
    },
    reference() {
      this.referenceMessage = true;
    },
    selectCard(item) {
      this.selectedObj = item
      if (this.selectedCard) {
        if (this.selectedCard === item.id) {
          this.selectedCard = null
          return;
        }
      }
      this.selectedCard = item.id

    },
    toggleMenu(e) {
      this.items.map(function (x) {
        if (x.id == e.id) {
          x.toggleMenu = !x.toggleMenu
        } else {
          x.toggleMenu = false;
        }
      });
    },
    closeMenus() {
      this.items.map(function (x) {
        x.toggleMenu = false;
        return;
      });

    },
  }
}
</script>
<style >
.card-select {
  overflow: visible;
}
</style>

#TODO: 
//disable by : listOneFull: false / listTwoFull: false, ok
//reference message
// component splitting
// refactoring
// select element logic !important ⚠️
// remove button General (board header)


