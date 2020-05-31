<template>
  <ul class="multiselect">
    <li
      v-for="select of selection"
      :key="select"
    >

      <label class="select" :class="{active: checked.includes(select)}">
        {{ select }}
        <input
          v-model="checked"
          :value="select"
          @change="$emit('update-selected', checked)"
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
    selected: Array
  },
  data () {
    return {
      checked: this.selected
    }
  }
}
</script>

<style scoped>
  input {
    display: none;
  }
  .multiselect {
    padding: 0;
    display: flex;
    list-style: none;
  }
  .select {
    margin: 5px;
    border: 1px solid #1D2D36;
    color: #1D2D36;
    border-radius: 7px;
    line-height: 19px;
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    padding: 5.5px 9.5px;
  }
  .active {
    background-color: #F5D734;
  }
</style>
