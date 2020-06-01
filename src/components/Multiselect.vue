<template>
  <ul class="selection">
    <li
      v-for="select of selection"
      :key="select"
    >
      <label class="select" :class="{active: currentSelected.includes(select)}">
        {{ select }}
        <input
          class="select__input"
          v-model="currentSelected"
          :value="select"
          @change="$emit('update-selected', currentSelected)"
          type="checkbox"
        >
      </label>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    selection: Array,
    selected: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      currentSelected: this.selected
    }
  }
}
</script>

<style scoped>
  .select__input {
    display: none;
  }
  .selection {
    display: flex;
    flex-wrap: wrap;
    padding: 0;
    margin: 0 27px 40px 52px;
    list-style: none;
  }
  .select {
    display: block;
    white-space: nowrap;
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
    font-weight: 400;
    line-height: 19px;
    margin: 5px 10px;
    padding: 5px 9px;
    cursor: pointer;
    color: #1d2d36;
    border: 1px solid #1d2d36;
    border-radius: 7px;
  }
  .active {
    background-color: #f5d734;
  }
</style>
