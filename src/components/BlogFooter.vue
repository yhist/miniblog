<template>
  <div class="clear-all-wrap">
    <span class="clear-all-bt" @click="clearAllMemo">
      Clear All
      <i class="fas fa-broom"></i>
    </span>
    <span class="copy">Copyright 2022 by Do Yeon Hee</span>
  </div>
</template>

<script>
  import {
    useStore
  } from 'vuex'
  export default {
    setup() {
      // vuex store 사용
      const store = useStore();
      const clearAllMemo = () => {
        // localStorage에서 내용 전체 삭제
        // 추후 DB연동 예정
        // localStorage.clear();
        // context.emit('deletememo')
        store.dispatch('fetchClearMemo');
      }
      return {
        clearAllMemo
      }
    }
  }
</script>

<style>
  .clear-all-wrap {
    position: relative;
    display: block;
    width: 100%;
    /* height: 50px; */
    line-height: 50px;
    background: #fff;
    text-align: center;
    margin: 0 auto;
    border-radius: 5px;
  }

  .clear-all-bt {
    display: inline-block;
    width: 80%;
    height: 50px;
    cursor: pointer;
    border: 1px solid pink;
    border-radius: 5px;
    margin: 10px;
    transition: background-color 0.5s;
  }

  .clear-all-bt:hover {
    background-color: pink;
    color: #fff;
  }

  .fa-broom {
    color: lightgrey;
  }

  .copy {
    display: block;
    font-size: 9px;
    white-space: nowrap;
  }
</style>