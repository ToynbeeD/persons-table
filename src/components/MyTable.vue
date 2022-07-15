<template>
  <div class="table">
    <div class="thead">
      <h2 class="th" @click="sortPersons('name')">Имя</h2>
      <h2 class="th" @click="sortPersons('phone')">Телефон</h2>
    </div>
    <ul class="tbody">
      <table-row
      v-for="person in firstLevelPersons"
      :key="person.id"
      :current-person="person"
      :persons="persons"
      />
    </ul>
  </div>
</template>

<script>
import TableRow from '@/components/TableRow.vue'
export default {
  components: { TableRow },
  props: {
    persons: Array
  },
  data () {
    return {
      sortDirection: false
    }
  },
  computed: {
    firstLevelPersons () {
      return this.persons.filter(person => !person.parentId)
    }
  },
  methods: {
    sortPersons (personKey) {
      const sortPersons = this.persons.sort((a, b) => {
        if (a[personKey].toLowerCase() > b[personKey].toLowerCase()) {
          return this.sortDirection ? -1 : 1
        }
        if (a[personKey].toLowerCase() < b[personKey].toLowerCase()) {
          return this.sortDirection ? 1 : -1
        }
        return 0
      })

      this.persons = sortPersons
      this.sortDirection = !this.sortDirection
    }
  }
}
</script>

<style scoped>
.table {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  width: 500px;
}

.thead, .tbody {
  width: 100%;
}

.thead {
  display: flex;
  padding: 20px;
  justify-content: space-between;
}

.th {
  cursor: pointer;
}

.th:not(:last-child) {
  margin-right: 20px;
}
</style>
