<template>
  <div class="notes">
    <div class="container">
        <div class="notes__top">
            <h2 class="notes__top-title">
                {{ notes.length > 0 ? 'Все заметки' : 'Нет заметок' }}
            </h2>
            <button class="notes__top-btn" @click="view = !view">
                <img src="@/assets/images/list.svg" alt="" v-show="view">
                <img src="@/assets/images/grid.svg" alt="" v-show="!view">
                <span>
                    {{ view ? 'Список' : 'Сетка' }}
                </span>
            </button>
        </div>
        <div class="notes__list" :class="{ active: !view }">
            <NotesItem 
                v-for="note in notes" 
                :key="note.id"
                :note="note"
                :view="view"
                @delNote="$emit('delNote', note.id)"
                @changeNote="$emit('changeNote', note.id)"
            />
        </div>
    </div>
  </div>
</template>

<script>

import NotesItem from '@/components/NotesItem.vue'


export default {
    components: {
      NotesItem  
    },
    data() {
        return {
            view: true
        }
    },
    props: {
        notes: Array
    }
}
</script>

<style>

</style>