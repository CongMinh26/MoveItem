<template>
  <b-container class="bv-example-row">
    <b-row>
      <b-col>
        <b-card-group deck>
          <b-card header="Task 1">
            <Task1
              v-for="item1 in ItemTask1"
              :key="item1"
              :item1="item1"
              :class="[item1.selected ? 'is-completed' : '']"
              @change-selected="Changeselected"
            >
            </Task1>
          </b-card>
        </b-card-group>
      </b-col>

      <b-col>
        <b-col><input type="submit" value=">" @click="MoveItemRight" /></b-col>
        <b-col><input type="submit" value="<" @click="MoveItemLeft" /></b-col>
        <b-col><input type="submit" value=">>"  /></b-col>
        <b-col><input type="submit" value="<<" /></b-col>
      </b-col>

      <b-col>
        <b-card-group deck>
          <b-card header="Task 2">
            <Task2
              v-for="item2 in ItemTask2"
              :key="item2"
              :item2="item2"
              :class="[item2.selected ? 'is-completed' : '']"
              @change-selected-2="Changeselected2"
            >
            </Task2>
          </b-card>
        </b-card-group>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import Task1 from "./Task1.vue";
import Task2 from "./Task2.vue";
export default {
  components: {
    Task1,
    Task2,
  },
  props:{
     listTask1: Array,
     listTask2: Array,
     listItemSelected: Array,

  },
  data() {
    return {
      ItemTask1: [
        {
          id: 1,
          title: "Item 1",
          selected: false,
        },
        {
          id: 2,
          title: "Item 2",
          selected: false,
        },
        {
          id: 3,
          title: "Item 3",
          selected: false,
        },
        {
          id: 4,
          title: "Item 4",
          selected: false,
        },
        {
          id: 5,
          title: "Item 5",
          selected: false,
        },
        {
          id: 6,
          title: "Item 6",
          selected: false,
        },
      ],
      ItemTask2: [
        {
          id: 9,
          title: "Item 9",
          selected: false,
        },
        {
          id: 10,
          title: "Item 10",
          selected: false,
        },
        {
          id: 11,
          title: "Item 11",
          selected: false,
        },
        {
          id: 12,
          title: "Item 12",
          selected: false,
        },
        {
          id: 13,
          title: "Item 13",
          selected: false,
        },
        {
          id: 14,
          title: "Item 14",
          selected: false,
        },
        {
          id: 15,
          title: "Item 15",
          selected: false,
        },
      ],
    };
  },
  methods: {
    Changeselected(item1) {
      const itemIndex = this.ItemTask1.indexOf(item1);
      this.ItemTask1[itemIndex].selected = !this.ItemTask1[itemIndex].selected;
    },
    Changeselected2(item2) {
      const itemIndex = this.ItemTask2.indexOf(item2);
      this.ItemTask2[itemIndex].selected = !this.ItemTask2[itemIndex].selected;
    },

    MoveItemRight() {
       var itemSelected = this.ItemTask1.filter(function (u) {
        return u.selected;
      });
     console.log(itemSelected);
      let i = 0;
      let j = 0;
      for (i; i < this.ItemTask1.length; i++) {
        for (j; j < itemSelected.length; j++) {
          if (itemSelected[j].id === this.ItemTask1[i].id) {
            this.ItemTask1.splice(this.ItemTask1[i], 1);
            this.ItemTask2.push(itemSelected[j]);
          }
        }
      }
      //this.ItemMove(this.ItemTask1,itemSelected,this.ItemTask2)
    },
    MoveItemLeft() {
       var itemSelected = this.ItemTask2.filter(function (u) {
        return u.selected;
      });
     console.log(itemSelected);
      let i = 0;
      let j = 0;
      for (i; i < this.ItemTask2.length; i++) {
        for (j; j < itemSelected.length; j++) {
          if (itemSelected[j].id === this.ItemTask2[i].id) {
            this.ItemTask2.splice(this.ItemTask2[i], 1);
            this.ItemTask1.push(itemSelected[j]);
          }
        }
      }
      //this.ItemMove(this.ItemTask1,itemSelected,this.ItemTask2)
    },
    

    // method dùng chung
    ItemMove(listTask1,listItemSelected,listTask2 ) {      
      let i = 0;
      let j = 0;
      for (i; i < listTask1.length; i++) {
        for (j; j < listItemSelected.length; j++) {
          if (listItemSelected[j].id === this.listTask1[i].id) {
            listTask1.splice(this.listTask1[i], 1);
            listTask2.push(listItemSelected[j]);
          }
        }
      }
    },

    
  },
};
</script>

<style>
.is-completed {
  text-decoration: line-through;
  background-color: rgb(219, 214, 214);
}
.input[type="button"],
input[type="submit"]{
  background-color: #349dd0;
  border: none;
  color: white;
  padding: 16px 32px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
}
.input[type="submit"]:hover{
  background-color: rgb(33, 209, 42);
}
</style>