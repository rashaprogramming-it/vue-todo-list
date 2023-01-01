<template>
      <header class="header">
        <Transition name="nav">
          <nav class="header__nav" v-show="header == true">
              <button class="header__nav-lang" style="display: none;">Ru</button>
              <h1 class="header__nav-title">Заметки</h1>
              <button class="header__nav-search" @click="header = false">
                  <img src="@/assets/images/search.svg" alt="">
              </button>
          </nav>
        </Transition>
         <Transition name="search">
          <nav class="header__search" v-show="header == false">
            <button class="header__search-back" @click="header = true, search = ''">
              <img src="@/assets/images/back.svg" alt="">
            </button>
            <input type="text" placeholder="Поиск..." v-model="search">
            <button class="header__search-clear" @click="search = ''">
              <img src="@/assets/images/close.svg" alt="">
            </button>
          </nav>
          </Transition>
      </header>
   
</template>

<script>
export default {
  data() {
    return {
      header: true,
      search: ''
    }
  },
  watch: {
    search(newVal) {
      this.$emit('setSearchVal', newVal)
    }
  }
}
</script>

