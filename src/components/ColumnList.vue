<template>
  <div class="row">
    <div class="col-4 mb-4" v-for="column in columnList" :key="column.id">
      <div class="card h-100 shadow-sm">
        <div class="card-body text-center">
          <img src="../assets/logo.png" class="card-img-top rounded-circle border border-light w-25 my-3" :alt="column.title">
          <h5 class="card-title ">{{column.title}}</h5>
          <p class="card-text text-start">{{column.description}}</p>
          <a href="#" class="btn btn-outline-primary">进入专栏</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
export interface ColumnProps {
  id: number;
  title: string;
  avatar: string;
  description: string;
}

export default defineComponent({
  name: 'ColumnList',
  props: {
    list: {
      type: Array as PropType<ColumnProps[]>,
      required: true
    }
  },
  setup (props) {
    const columnList = computed(() => {
      return props.list.map(item => {
        if (!item.avatar) {
          item.avatar = '/img/logo.82b9c7a5.png'
        }
        return item
      })
    })

    return {
      columnList
    }
  }
})
</script>

<style scoped>

</style>
