<template>
  <Transition name="modal">
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h2 class="modal__block-title">
            {{ edit ? 'Изменить заметку' : 'Добавить заметку' }}
        </h2>
        <div class="modal__block-inputs">
          <label>
            <span>Title</span>
            <input type="text" v-model.trim="title" />
          </label>
          <label>
            <span>Content</span>
            <textarea v-model.trim="text"></textarea>
          </label>
        </div>
        <div class="modal__block-btns">
          <button class="modal__block-btn del" @click="closeModal">
            Отмена
          </button>
          <button v-if="!edit" class="modal__block-btn edit" @click="addNote">
            Добавить
          </button>
          <button v-else class="modal__block-btn edit" @click="editeNote">
            Изменить
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: {
    edit: Boolean,
    editedNote: Object
  },
  data() {
    return {
      title: "",
      text: "",
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
      this.title = this.text = "";
    },
    addNote() {
      if (this.title != "" && this.text != "") {
        const note = {
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", note);
        this.title = this.text = "";
      }
    },
    editeNote() {
     if(this.title != '' && this.text != '') {
        const editNote = {
          id: this.editedNote.id,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString()
        }
        this.$emit('editeNewNote', editNote)
        this.closeModal()

     }
    }
  },
};
</script>

<style>
</style>