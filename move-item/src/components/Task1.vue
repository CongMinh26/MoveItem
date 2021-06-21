<template>
  <b-list-group-item>
    <input type="checkbox" :checked="item1.selected" @change="Changeselected(item1)"/>
    {{ item1.title }}
  </b-list-group-item>
</template>

<script>
export default {
  props:['item1'],
  methods: {
    Changeselected(item1) {
      console.log(item1)
      this.$emit("change-selected", item1);
    },
  },
};
</script>

<style>
.is-completed {
  text-decoration: line-through;
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