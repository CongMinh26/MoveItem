<template>
  <b-list-group-item>
    <input type="checkbox" :checked="item2.selected" @change="Changeselected2(item2)"/>
    {{ item2.title }}
  </b-list-group-item>
</template>

<script>
export default {
  props:['item2'],
  methods: {
    Changeselected2(item2) {
      console.log(item2)
      this.$emit("change-selected-2", item2);
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
  padding: 13px 20px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
}
</style>