<template>
  <div class="container">
    <virtual-list
      :item-size="60"
      :items="rows"
      v-slot="{ item }"
    >
      <div class="row">
        <div
          v-for="square in item.squares"
          :key="square.id"
          class="square"
          :style="square.style"
          @mouseover="handleMouseOver($event)"
          @mouseleave="handleMouseLeave($event)"
        >
          {{ square.value }}
        </div>
      </div>
    </virtual-list>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import { VirtualList } from 'vueuc';

export default defineComponent({
  components: {
    VirtualList
  },
  data() {
    return {
      rows: this.generateRows(100000)
    };
  },
  methods: {
    generateRows(count) {
      let rows = [];
      for (let i = 0; i < count; i++) {
        let squares = [];
        let squareCount = Math.floor(Math.random() * 11) + 10;
        for (let j = 0; j < squareCount; j++) {
          squares.push({
            id: `square-${i}-${j}`,
            value: Math.floor(Math.random() * 101),
            style: {
              width: '50px',
              height: '50px',
              borderRadius: `${Math.floor(Math.random() * 51)}px`,
              backgroundColor: 'rgb(60, 60, 60)',
              color: 'white',
              display: 'flex',
              alignItems: 'center',
              justifyContent: 'center',
              margin: '5px',
              transition: 'transform 0.2s'
            }
          });
        }
        rows.push({ id: `row-${i}`, squares });
      }
      return rows;
    },
    handleMouseOver(event) {
      event.target.style.transform = 'scale(0.8)';
    },
    handleMouseLeave(event) {
      event.target.style.transform = 'scale(1)';
    }
  }
});
</script>

<style>
.container {
  height: 100vh;
  overflow: hidden;
}

.row {
  display: flex;
}

.square {
  transition: transform 0.2s;
}
</style>
