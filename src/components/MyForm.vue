<template>
  <form class="modal__form form" action="#">
    <label class="form__label">
      <span class="form__label-span">Имя*</span>
      <input v-model="personName" class="form__label-input" type="text" />
    </label>
    <label class="form__label">
      <span class="form__label-span">Телефон*</span>
      <input v-model="personPhone" class="form__label-input" type="text" />
    </label>
    <label class="form__label">
      <span class="form__label-span">Начальник</span>
      <select class="form__label-select" name="parent" v-model="parentId">
        <option value="" selected disabled></option>
        <option
          v-for="person in persons"
          :key="person.id"
          :value="person.id"
        >
          {{ person.name }}
        </option>
      </select>
    </label>
    <p v-if="isHasError" class="form__error">Заполните обязательные поля</p>
    <button class="form__submit btn" type="submit" @click.prevent="createNewPerson">Сохранить</button>
  </form>
</template>

<script>
export default {
  props: {
    persons: Array
  },
  data () {
    return {
      personName: '',
      personPhone: '',
      parentId: null,
      isHasError: false
    }
  },
  methods: {
    createNewPerson () {
      if (!this.personName.trim() || !this.personPhone.trim()) {
        this.isHasError = true
        return
      }
      this.isHasError = false

      const person = {
        id: Date.now(),
        name: this.personName.trim(),
        phone: this.personPhone.trim(),
        parentId: this.parentId
      }
      this.$emit('addPerson', person)

      this.personName = ''
      this.personPhone = ''
      this.parentId = null
    }
  }
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 400px
}

.form__label {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.form__submit {
  font-size: 16px;
  font-weight: bold;
}

.form__label-input,
.form__label-select {
  width: 230px;
  height: 30px;
}

.form__submit {
  align-self: center;
  padding: 10px 20px;
  border: 1px solid #000;
  transition: background-color .2s linear;
}

.form__submit:hover {
  background-color: #c4c4c4;
}

.form__error {
  margin-bottom: 10px;
  color: red;
  font-size: 14px;
}
</style>
