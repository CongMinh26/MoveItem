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
              :class="item1.selected ? 'is-completed' : ''"
              @change-selected="changeSelected"
            >
            </Task1>
          </b-card>
        </b-card-group>
      </b-col>

      <b-col>
        <b-col><input type="submit" value="^" @click="moveUp" /></b-col>
        <b-col><input type="submit" value="v" @click="moveDown" /></b-col>
        <b-col><input type="submit" value=">" @click="moveRight" /></b-col>
        <b-col><input type="submit" value="<" @click="moveLeft" /></b-col>
      </b-col>

      <b-col>
        <b-card-group deck>
          <b-card header="Task 2">
            <Task2
              v-for="item2 in ItemTask2"
              :key="item2"
              :item2="item2"
              :class="item2.selected ? 'is-completed' : ''"
              @change-selected-2="changeSelected2"
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
  props: {
    list: Array,
    listTask1: Array,
    listTask2: Array,
    listItemSelected: Array
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
    changeSelected(item1) {
      const itemIndex = this.ItemTask1.indexOf(item1);
      this.ItemTask1[itemIndex].selected = !this.ItemTask1[itemIndex].selected;
    },
    changeSelected2(item2) {
      const itemIndex = this.ItemTask2.indexOf(item2);
      this.ItemTask2[itemIndex].selected = !this.ItemTask2[itemIndex].selected;
    },

    moveRight() {
      var itemSelected = this.ItemTask1.filter(function (u) {
        return u.selected;
      });
      this.ItemTask2 = this.ItemTask2.concat(itemSelected);
      this.ItemTask2 = this.ItemTask2.map((obj) => {
        return {
          ...obj,
          selected: false,
        };
      });
      this.ItemTask1 = this.ItemTask1.filter((item) => {
        return !item.selected;
      });
    },
    moveLeft() {
      var itemSelected = this.ItemTask2.filter(function (u) {
        return u.selected;
      });
      this.ItemTask1 = this.ItemTask1.concat(itemSelected);
      this.ItemTask1 = this.ItemTask1.map((obj) => {
        return {
          ...obj,
          selected: false,
        };
      });
      this.ItemTask2 = this.ItemTask2.filter((item) => {
        return !item.selected;
      });
    },
    moveUp() {
      this.up(this.ItemTask1);  
    },
    
    moveDown() {
     this.down(this.ItemTask1)
    },

    //method
    up(list){
      let temp =0
      for (let i = 0; i < list.length; i++) {
        if (list[i].selected === true && (i-1) >= 0) {
          temp = i;
        }
      }
      list.splice(temp - 1, 0, list.splice(temp, 1)[0]);
    },
    down(list){
      let temp =0
      for (let i = 0; i <= list.length; i++) {
        if (list[i].selected === true) {
          temp = i;
        }
      }
      list.splice(temp + 1, 0, list.splice(temp, 1)[0]);
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
input[type="submit"] {
  background-color: #349dd0;
  border: none;
  color: white;
  padding: 16px 32px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
}
.input[type="submit"]:hover {
  background-color: rgb(33, 209, 42);
}
</style>