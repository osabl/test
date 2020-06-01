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
    margin: 0 41px 40px 51px;
    list-style: none;
  }
  .select {
    display: block;
    white-space: nowrap;
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
    font-weight: 400;
    line-height: 19px;
    margin: 4.5px 10px;
    padding: 5px 9px;
    cursor: pointer;
    color: #1d2d36;
    border: 1px solid #1d2d36;
    border-radius: 7px;
  }
  .active {
    background-color: #f5d734;
  }

  /* FOR PIXEL PERFECT :) */
  .selection li:nth-child(1) .select {
    margin-right: 6px;
    padding-right: 11px;
  }
  .selection li:nth-child(2) .select {
    margin-right: 2px;
    padding-right: 13px;
    padding-left: 6px;
  }
  .selection li:nth-child(3) .select {
    margin-right: 0px;
  }
  .selection li:nth-child(4) .select {
    padding-right: 12px;
  }
  .selection li:nth-child(5) .select {
    margin-right: 3px;
  }
  .selection li:nth-child(6) .select {
    margin-right: 2px;
    padding-right: 13px;
  }
  .selection li:nth-child(7) .select {
    margin-right: 3px;
    padding-right: 10px;
  }
  .selection li:nth-child(8) .select {
    padding-right: 11px;
  }
</style>
