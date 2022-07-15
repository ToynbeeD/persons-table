<template>
  <div class="modal">
    <div class="modal__body">
      <h2 class="modal__heading">Добавление пользователя</h2>
      <my-form @addPerson="addPerson" :persons="persons"/>
      <button class="modal__close btn" @click="removeModal">X</button>
    </div>
  </div>
</template>

<script>
import MyForm from '@/components/MyForm.vue'

export default {
  components: {
    MyForm
  },
  props: {
    persons: Array
  },
  methods: {
    removeModal () {
      this.$emit('remove')
    },
    addPerson (person) {
      this.$emit('addPerson', person)
    }
  }
}
</script>

<style scoped>
.modal {
  position: absolute;
  display: flex;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  background-color: rgb(0, 0, 0, .5);
}

.modal__body {
  position: relative;
  padding: 20px;
  background-color: #fff;
}

.modal__heading {
  margin-bottom: 30px;
}

.modal__close {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  line-height: 100%;
  font-weight: bold;
  transition: color .2s linear;
}

.modal__close:hover {
  color: brown;
}
</style>
