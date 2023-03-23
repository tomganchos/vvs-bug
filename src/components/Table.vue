<template>
<div
    ref="scrollerContainer"
    class="scroller-container"
>
  <header ref="header">
    <div class="dynamic-columns">
      <div
          v-for="(column, index) in columns"
          :key="'header' + column.key + index"
          class="header-cell"
      >
        <span>{{ column.title }}</span>
      </div>
    </div>
  </header>
  <recycle-scroller
    v-slot="{ item }"
    ref="recycleScroller"
    class="scroller"
    :items="data"
    :item-size="height"
    :key-field="keyField"
    >
    <div class="row">
      <div
          class="dynamic-columns"
      >
        <div
            v-for="(column, index) in columns"
            :key="item.id + column.key + index"
            class="cell"
            :data-column="column.key"
        >
          <slot
              :name="`row-${column.key}`"
              :item="item"
          >
            <span>{{ item[column.key] }}</span>
          </slot>
        </div>
      </div>
    </div>
  </recycle-scroller>
</div>
</template>

<script>
export default {
  name: "Table",
  props: {
    data: {
      type: Array,
      default: () => []
    },
    columns: {
      type: Array,
      default: () => []
    },
    height: {
      type: Number,
      default: 32
    },
    keyField: {
      type: String,
      default: 'id',
    },
    scroll: {
      type: Number
    }
  },
  data () {
    return {
      elScrollLeft: 0,
      scrollLeft: 0,
      elem: null
    }
  },
  watch: {
    'scroll': function(value) {
      const { recycleScroller } = this.$refs
      recycleScroller.$el.querySelectorAll('.dynamic-columns').forEach(el => {
        el.scrollLeft = value
      })
      this.$refs.header.querySelector('.dynamic-columns').style.transform = `translate(${(-value)}px, 0)`
    },
  },
  mounted() {
    this.$nextTick(() => {
      this.handleScrolls()
    })
  },
  methods: {
    handleScrolls () {
      this.$nextTick(() => {
        const { recycleScroller } = this.$refs
        if (recycleScroller.$el && recycleScroller.$el.querySelectorAll('.dynamic-columns')) {
          recycleScroller.$el.querySelectorAll('.dynamic-columns').forEach(el => {
            el.addEventListener('mousedown', this.eventMousedown)
            el.addEventListener('mouseleave', this.eventMouseleave)
            el.addEventListener('mouseenter', this.eventMouseenter)
            el.addEventListener('mousemove', this.eventMousemove)
          })
          window.addEventListener('mouseup', this.eventMouseup)
        }
      })

    },

    eventMousedown (e) {
      let el = this.getElement(e)
      this.isDown = true
      el.classList.add('active')
      this.$refs.recycleScroller.$el.classList.add('active')
      this.startX = e.pageX - el.offsetLeft
      this.elScrollLeft = el.scrollLeft
    },
    eventMouseleave (e) {
      let el = this.getElement(e)
      el.classList.remove('active')
    },
    eventMouseenter (e) {
      let el = this.getElement(e)
      if(!this.isDown) return;
      el.classList.add('active');
      this.startX = e.pageX - el.offsetLeft;
      this.elScrollLeft = el.scrollLeft;

      e.preventDefault();
      const x = e.pageX - el.offsetLeft;
      const walk = (x - this.startX);
      // console.log('walk', walk)
      el.scrollLeft = this.elScrollLeft - walk
      // this.elem.scrollLeft = this.elScrollLeft - walk;
      this.$refs.header.querySelector('.dynamic-columns').style.transform = `translate(${(-el.scrollLeft)}px, 0)`
      const element = e.path[0]
      this.$refs.recycleScroller.$el.querySelectorAll('.dynamic-columns').forEach(elem => {
        if (!element.isEqualNode(elem)) {
          elem.style.transform = `translate(${(elem.scrollLeft)}px, 0)`
        }
      })
    },

    eventMouseup (e) {
      // console.log('eventMouseup')
      let el = this.getElement(e)
      if (el) {
        this.elScrollLeft = el.scrollLeft
      }
      this.isDown = false;
      if (this.$refs.recycleScroller && this.elem) {
        this.$refs.recycleScroller.$el.classList.remove('active')
        this.elem.classList.remove('active');
      }
    },

    eventMousemove (e) {
      let el = this.getElement(e)
      if(!this.isDown) return;
      e.preventDefault();
      const x = e.pageX - el.offsetLeft;
      const walk = (x - this.startX);
      // this.elem.scrollLeft = this.elScrollLeft - walk;
      el.scrollLeft = this.elScrollLeft - walk
      this.$refs.header.querySelector('.dynamic-columns').style.transform = `translate(${(-el.scrollLeft)}px, 0)`
      // const element = e.path.find(elem => elem._prevClass === 'dynamic-columns')
      const { clientWidth, scrollLeft, scrollWidth } = this.$refs.recycleScroller.$el.querySelector('.dynamic-columns')
      this.$refs.recycleScroller.$el.querySelectorAll('.dynamic-columns').forEach(elem => {
        if (!el.isEqualNode(elem)) {
          elem.scrollLeft = el.scrollLeft
        }
      })
      // this.shadow.left = scrollLeft !== 0
      // this.shadow.right = scrollWidth !== Math.round(clientWidth + scrollLeft)
    },

    getElement (elem) {
      if (elem.target.classList.contains('dynamic-columns')) {
        return elem.target
      } else if (elem.target.parentNode.classList.contains('dynamic-columns')) {
        return elem.target.parentNode
      } else if (elem.target.parentNode.parentNode.classList.contains('dynamic-columns')) {
        return elem.target.parentNode.parentNode
      }
    }
  }
}
</script>

<style scoped>
 .scroller-container {
   overflow: hidden;
 }
 header {
   display: flex;
   font-style: normal;
   font-weight: 400;
   height: 32px;
   color: #6b6e8d;
   background: #fff;
   overflow: hidden;
 }
 header .dynamic-columns {
   flex-grow: 1;
   display: grid;
   grid-template-columns: 100px 200px 200px 400px;
 }
 .scroller {
   height: calc(100% - 32px);
   overflow-y: auto;
   overflow-x: hidden;
 }
 .scroller .dynamic-columns {
   display: grid;
   grid-template-columns: 100px 200px 200px 400px;
   cursor: grab;
   flex-grow: 1;
   overflow-x: hidden;
 }
 .cell {
   height: 32px;
 }
 .row {
   display: flex;
   overflow: hidden;
   font-style: normal;
   height: 32px;
   color: #474b6d;
 }

 :deep(.vue-recycle-scroller__item-wrapper) {
   position: relative;
   width: 100%!important;
   box-sizing: border-box;
   overflow: hidden;
 }
 :deep(.vue-recycle-scroller__item-view) {
   position: absolute;
   top: 0;
   left: 0;
   will-change: transform;
   width: 100%;
 }
</style>
