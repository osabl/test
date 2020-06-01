<template>
  <div>
    <button class="close" @click="$emit('close')"></button>
    <h2 class="title">have something to write?</h2>
    <textarea class="message" v-model="currentMessage"></textarea>
    <button class="btn btn-submit" @click="$emit('update-message', currentMessage)" type="submit">submit</button>
    <button class="btn btn-prev" @click="$emit('prev')"></button>
  </div>
</template>

<script>

export default {
  props: {
    message: String
  },
  data () {
    return {
      currentMessage: this.message
    }
  }
}
</script>

<style scoped>
  .close {
    display: block;
    width: 24px;
    height: 24px;
    margin: 8px 11px 0 auto;
    cursor: pointer;
    border: none;
    background-color: transparent;
    background-image: url(../assets/close.svg);
    background-repeat: no-repeat;
    background-position: center;
    background-size: 14px;
  }
  .title {
    font-family: 'Roboto', sans-serif;
    font-size: 26px;
    font-weight: 700;
    line-height: 32px;
    margin-top: 3px;
    margin-bottom: 8px;
    padding-left: 13px;
  }
  .message {
    display: block;
    width: 594px;
    height: 108px;
    margin: 0 50px;
    resize: none;
    border: 1px solid #e0e0e0;
  }
  .btn-submit {
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
    font-weight: 700;
    display: block;
    margin: 19px auto;
    padding: 11px 33px 10px 33px;
    cursor: pointer;
    border: none;
    border-radius: 4px;
    background-color: #ffe000;
  }
  .btn-prev {
    width: 70px;
    height: 50px;
    margin-bottom: 16px;
    cursor: pointer;
    border: none;
    background-color: #8d9599;
    background-image: url(../assets/arrow.svg);
    background-repeat: no-repeat;
    background-position: center;
  }
</style>
