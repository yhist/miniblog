<template>
  <div class="list-wrap">
    <TransitionGroup name="list" tag="ul">
    <!-- <ul> -->
      <!-- v-for in :key -->
      <li v-for="(item, index) in memodata" v-bind:key="index" class="shadow">
        <i class="fas fa-check-circle check-bt" @click="updateMemo(item, index)"
          :class="{memoComplete:item.complete}"></i>
        <span :class="{memoCompleteTxt:item.complete}">{{item.memotitle}}</span>
        <div class="info">
          <span class="icon" :style="{backgroundImage:'url(' + require(`@/assets/images/${item.memoicon}`) + ')'}"></span>
          <span class="date">{{item.memodate}}</span>
          <span class="remove-bt" @click="removeMemo(item.id, index)">
            <i class="fas fa-trash-alt"></i>
          </span>
        </div>
      </li>
    <!-- </ul> -->
  </TransitionGroup>
  </div>
</template>

<script>
  export default {
    props: ['memodata'],
    setup(props, context) {

      const removeMemo = (item, index) => {
        context.emit('removeitem', item, index)
      }

      const updateMemo = (item, index) => {
        context.emit('updateItem', item, index);
      }

      return {
        removeMemo,
        updateMemo,
      }
    }

  }
</script>

<style>
  li {
    display: flex;
    min-height: 50px;
    line-height: 50px;
    margin: 10px 0;
    background: #fff;
    border-radius: 5px;
    padding: 0 20px;
  }

  .info {
    margin-left: auto;
  }
  .icon {
    display: inline-block;
    width: 40px;
    height: 40px;
    margin-right: 10px;
    margin-top: 10px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
  }
  .date {

  }
  .remove-bt {
    margin-left: 10px;
    color: pink;
    cursor: pointer;
  }

  .check-bt {
    color: lightskyblue;
    line-height: 50px;
    margin-right: 10px;
    cursor: pointer;
  }

  .memoComplete {
    color: #b3adad;
  }

  .memoCompleteTxt {
    color: #b3adad;
    text-decoration: line-through;
  }

  /* 애니메이션 */
  .list-enter-active,
  .list-leave-active {
    transition: all 0.5s ease;
  }
  .list-enter-from,
  .list-leave-to {
    opacity: 0;
    transform: translateX(50px);
  }
</style>