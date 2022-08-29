<template>
  <div class="input-wrap shadow">
    <input type="text" v-model="newItem" class="input-box" maxlength="45" @keyup.enter="addItem">
    <!-- <button v-on:click="addItem">추가</button> -->
    <span @click="addItem" class="add-bt">
      <i class="fas fa-plus add-bt-icon"></i>
    </span>
  </div>
</template>

<script>
  import { ref } from 'vue'
  export default {
    setup() {
      const newItem = ref('');
      // 현재 시간값을 계산ㅎㅐ서 중복이 되지 않는 값을 처리한다.
      // 용도는 key와 id를 생성해 주기 위해서 처리
      // 10보다 작은 값에 0을 붙임
      const addZero = (n) => {
        return n < 10 ? '0' + n : n;
      }
      // 현재 시간을 리턴
      const getCurrentDate = () => {
        let date = new Date();
        return date.getFullYear().toString() + addZero(date.getMonth() + 1) + addZero(date.getDate()) +
          addZero(date.getHours()) + addZero(date.getMinutes()) + addZero(date.getSeconds());
      }
      const addItem = () => {
        let temp = newItem.value;

        // 앞쪽 뒤쪽 공백 제거
        temp = temp.trim()
        // 추우 업데이트 예정 (정규 표현식-문자열체크 문법)
        // 공백  공백   뒷자리 공백
        if (temp !== '') {
          // localStorage.setItem(키, 값);
          // 값은 추후에 json 형태로 만들어서 저장
          // JSON.stringify(오브젝트)
          // localStorage.setItem(키, json 문자열로 저장);
          // JSON저장 문자열
          /*
            {completed: false, title: 메모내용, icon:파일명}
          */
          let memoTemp = {
            id: getCurrentDate(),
            complete: false,
            memotitle: newItem.value,
            // memoicon: 'ico.png',
            // memodate: new Date(),
            // memocate: 'memo[info]',
            // memourl: 'a.html',
            // memopic: 'a.jpg',
          };

          // 추후 실제 DB 연동 예정
          localStorage.setItem(memoTemp.id, JSON.stringify(memoTemp));
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