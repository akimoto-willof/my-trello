<template>
  <div>
      <header>
          my Trello
          <div class="image-bg">
              <button>背景を設定する</button>
          </div>
      </header>
      <main>
            <p class="info-line">All: {{ totalCardCount }} tasks</p>
            <draggable :list="lists"
                class="list-index"
                @end="movingList"
                >
                <list v-for="(item, index) in lists"
                    :key="item.id"
                    :title="item.title"
                    :cards="item.cards"
                    :listIndex="index"
                    @change="movingCard"
                />
            <list-add />
            </draggable>
      </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import List from './List.vue'
import ListAdd from './ListAdd'
import { mapState } from 'vuex'

export default {
    components: {
        draggable,
        ListAdd,
        List
    },
    computed: {
        ...mapState([
            'lists'
        ]),
        totalCardCount(){
            return this.$store.getters.totalCardCount
        },
    },
    methods: {
        movingCard(){
            this.$store.dispatch('updateList', { lists: this.lists })
        },
        movingList(){
            this.$store.dispatch('updateList', { lists: this.lists })
        }
    }
}
</script>

<style>

</style>