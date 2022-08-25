<template>
  <div class="input-wrap shadow">
    <input type="text" v-model="newItem" class="input-box" maxlength="30" @keyup.enter="addItem">
    <!-- <button v-on:click="addItem">추가</button> -->
    <span @click="addItem" class="add-bt">
      <i class="fas fa-plus add-bt-icon"></i>
    </span>
  </div>
</template>

<script>
  import {
    ref
  } from 'vue'
  export default {
    setup() {
      const newItem = ref('');
      const addItem = () => {
        let temp = newItem.value;

        // 앞쪽 뒤쪽 공백 제거
        temp = temp.trim()
        if (temp !== '') {
          // localStorage.setItem(키, 값);
          // localStorage.setItem(키, json 문자열로 저장);
          // JSON저장 문자열
          /*
            {completed: false, title: 메모내용, icon:파일명}
          */
          localStorage.setItem(temp, temp);
          resetItem();
        }
        
      }
      // 내용 재설정 
      const resetItem = () => {
        newItem.value = '';
      }
      return {
        newItem,
        addItem
      }
    }
  }
</script>

<style scoped>
  .input-wrap{
    position: relative;
    display: block;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
    background: #fff;
    overflow: hidden;
    margin: 20px 0;
  }
  .input-wrap input {
    border-style: none;
  }
  .input-wrap input:focus {
    outline: none;
  }
  .input-box {
    width: 70%;
    font-size: 15px;
    margin-left: 20px;
    color: gray;
  }
  .add-bt {
    display: block;
    float: right;
    background: pink;
    cursor: pointer;
  }
  .add-bt-icon {
    display: inline-block;
    vertical-align: middle;
    color: #fff;
    cursor: pointer;
    margin: 0 20px;
  }
</style>