<template>
    <div class="notes__item">
        <div class="notes__item-top" :class="{ between : !view}">
            <h3 class="notes__item-title">{{ note.title }}</h3>
            <p class="notes__item-date">{{ note.date }}</p>
        </div>
        <p class="notes__item-text">{{ note.text }}</p>
        <div class="notes__item-btns">
            <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
                <img src="@/assets/images/edit.svg" alt="">
                <span>РЕДАКТИРОВАТЬ</span>
            </button>
            <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
                <img src="@/assets/images/del.svg" alt="">
                <span>Удалить</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        note: Object,
        view: Boolean
    }
}
</script>

<style>

</style>