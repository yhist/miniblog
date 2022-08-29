<template>
  <div class="input-wrap shadow">
    <input type="text" v-model="newItem" class="input-box" maxlength="45" @keyup.enter="addItem">
    <!-- <button v-on:click="addItem">추가</button> -->
    <div class="option">
      <span @click="addIcon(0)" class="img1">이미지1</span>
      <span @click="addIcon(1)" class="img2">이미지2</span>
      <span @click="addIcon(2)" class="img3">이미지3</span>
      <span @click="addItem(1)" class="add-bt">
        <i class="fas fa-plus add-bt-icon"></i>
      </span>
    </div>
  </div>
</template>

<script>
  import {
    ref
  } from 'vue'
  export default {
    setup(props, context) {
      const newItem = ref('');
      const newIcon = ref(0);

      const addItem = () => {
        let temp = newItem.value;
        let icon = newIcon.value;

        // 앞쪽 뒤쪽 공백 제거
        temp = temp.trim()
        // 추우 업데이트 예정 (정규 표현식-문자열체크 문법)
        // 공백  공백   뒷자리 공백
        if (temp !== '') {
          // 추후 실제 DB 연동 예정
          context.emit("additem", temp, icon);
          resetItem();
        }

      }
      // 내용 재설정 
      const resetItem = () => {
        newItem.value = '';
      }

      const addIcon = (index) => {
        console.log(index);
        newIcon.value = index;
      }

      return {
        newItem,
        addItem,
        addIcon,
      }
    }
  }
</script>

<style scoped>
  .input-wrap {
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
    width: calc(93% -250px);
    font-size: 15px;
    margin-left: 20px;
    color: gray;
  }

  .option {
    position: absolute;
    display: block;
    right: 0;
    top: 0;
  }

  .img1:active {
    outline: 3px solid lightpink;
  }
  .img2:active {
    outline: 3px solid lightpink;
  }
  .img3:active {
    outline: 3px solid lightpink;
  }

  .img1 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    margin-right: 10px;
    background: url('@/assets/images/dog.png') no-repeat center;
    background-size: cover;
    cursor: pointer;
  }

  .img2 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    margin-right: 10px;
    background: url('@/assets/images/dog2.png') no-repeat center;
    background-size: cover;
    cursor: pointer;
  }

  .img3 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    background: url('@/assets/images/dog3.png') no-repeat center;
    background-size: cover;
    cursor: pointer;
  }

  .add-bt {
    display: inline-block;
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