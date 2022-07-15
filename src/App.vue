<template>
  <div id="app">
    <button class="add-btn btn" @click="openModal">Добавить</button>
    <p class="message-empty" v-if="persons.length === 0">
      Вы ещё не добавили пользователей...
    </p>
    <my-table v-else :persons="persons" />
    <my-modal
      @remove="closeModal"
      @addPerson="addNewPerson"
      :persons="persons"
      v-if="isModalActive"
    />
  </div>
</template>

<script>
import MyModal from '@/components/MyModal.vue'
import MyTable from '@/components/MyTable.vue'
export default {
  name: 'App',
  components: {
    MyModal,
    MyTable
  },
  data () {
    return {
      isModalActive: false,
      persons: []
    }
  },
  methods: {
    openModal () {
      this.isModalActive = true
    },
    closeModal () {
      this.isModalActive = false
    },
    addNewPerson (person) {
      this.persons.push(person)
      localStorage.setItem('personsData', JSON.stringify(this.persons))
    },
    getLocaleStorageData () {
      const personsData = localStorage.getItem('personsData')
      if (personsData) {
        this.persons = JSON.parse(personsData)
      } else {
        this.persons = []
      }
    }
  },
  created () {
    this.getLocaleStorageData()
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
}

#app {
  padding: 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  width: 100vw;
  height: 100vh;
}

ul {
  list-style: none;
}

.btn {
  padding: 0;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.add-btn {
  margin-bottom: 30px;
  padding: 15px 30px;
  border: 1px solid #000;
  border-radius: 10px;
  font-size: 20px;
  font-weight: 600;
  transition-property: background-color color;
  transition-duration: .2s;
  transition-timing-function: linear;
}

.add-btn:hover {
  background-color: navy;
  color: #fff;
}

.message-empty {
  font-size: 24px;
}
</style>
