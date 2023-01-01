<template>
  <div class="wrapper">
    <Navbar
      @setSearchVal="search = $event"
    />
    <Notes 
      :notes="filterNotes"
      @delNote="delNote"
      @changeNote="changeNote"
    />
    <Modal 
      v-show="isModalOpen"
      @closeModal="isModalOpen = false, edit = false"
      @addNote="addNote"
      :edit="edit"
      :editedNote="editedNote"
      @editeNewNote="editeNewNote"
    />
    <button class="add__note" @click="isModalOpen = true" v-if="!isModalOpen">
      <img src="@/assets/images/edit.svg" alt="">
    </button>
  </div>
</template>

<script>

import Navbar from '@/components/Navbar.vue'
import Notes from '@/components/Notes.vue'
import Modal from '@/components/Modal.vue'

export default {
  components: {
    Navbar,
    Notes,
    Modal
  },
  data() {
    return {
      search: '',
      edit: false,
      isModalOpen: false,
      currentId: 1,
      notes: [],
      editedNote: null
    }
  },
  mounted() {
    this.getNotes()
  },
  computed: {
    filterNotes() {
      return this.search ? this.notes.filter(note => note.title.toLowerCase().includes(this.search.toLowerCase())) : this.notes
    }
  },
  methods: {
    addNote(note) {
      note.id = this.currentId++
      this.notes.push(note)
      this.isModalOpen = false
    },
    delNote(id) {
      let idx = this.notes.findIndex(note => note.id == id)
      this.notes.splice(idx, 1)
    },
    getNotes() {
      const localNotes = localStorage.notes
      if(localNotes) {
        this.notes = JSON.parse(localNotes)
      }
    },
    changeNote(id) {
      this.isModalOpen = this.edit = true
      let currentNote = this.notes.find(note => note.id == id)
      this.editedNote = currentNote
    },
    editeNewNote(noteEdit) {
      this.notes.forEach(note => {
        if(note.id == noteEdit.id) {
          note.title = noteEdit.title
          note.text = noteEdit.text
          note.date = noteEdit.date
        }
      })
    },
  },
  watch: {
    notes: {
      handler() {
        localStorage.notes = JSON.stringify(this.notes)
      },
      deep: true
    }
  }
}
</script>

