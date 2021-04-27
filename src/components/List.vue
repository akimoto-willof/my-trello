<template>
    <div class="list" :class="{rotate:listRotateStart}">
        <div class="listheader">
            <p class="list-title">{{ title }}</p>
            <p class="list-counter">total: {{ totalCardInList }}</p>
            <div class="deletelist" @click="removeList">×</div>
        </div>
        <draggable group="cards"
            :list="cards"
            @end="$emit('change')"
            >
        <card v-for="(item, index) in cards"
            :body="item.body"
            :key="item.id"
            :cardIndex="index"
            :listIndex="listIndex"
        />
        <card-add :listIndex="listIndex" />
        </draggable>
        </div>
</template>

<script>
import draggable from 'vuedraggable'
import CardAdd from './CardAdd'
import Card from './Card'

export default {
    components: {
        draggable,
        CardAdd,
        Card
    },
    props:{
        title: {
            type: String,
            require: true
        },
        cards: {
            type: Array,
            required: true
        },
        listIndex: {
            type: Number,
            required: true
        }
    },
    data(){
        return {
            listRotateStart: false
        }
    },
    computed: {
        totalCardInList(){
            return this.cards.length
        }
    },
    methods: {
        removeList(){
            if(confirm('本当にこのリストを削除しますか？')){
                this.$store.dispatch('removelist',{ listIndex: this.listIndex })
            }
        }
    }

}
</script>

