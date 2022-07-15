<template>
  <li class="tr">
    <div class="td name">
      <button class="open-btn btn"
        v-if="personChildren.length > 0"
        @click="changeChildActiveStatus"
      >
        {{ openBtnIcon }}
      </button>
      {{ currentPerson.name }}
    </div>
    <div class="td phone">{{ currentPerson.phone }}</div>
    <ul v-show="isChildActive" class="child-wrapper">
      <table-row class="tr"
        v-for="childPerson in personChildren"
        :key="childPerson.id"
        :persons="persons"
        :current-person="childPerson"
      >
        <div class="td name">{{ childPerson.name }}</div>
        <div class="td phone">{{ childPerson.phone }}</div>
      </table-row>
    </ul>
  </li>
</template>
<script>
export default {
  name: 'table-row',
  props: {
    persons: Array,
    currentPerson: Object
  },
  data () {
    return {
      isChildActive: false
    }
  },
  computed: {
    personChildren () {
      return this.persons.filter(person => person.parentId === this.currentPerson.id)
    },
    openBtnIcon () {
      if (this.isChildActive) return '-'
      return '+'
    }
  },
  methods: {
    changeChildActiveStatus () {
      this.isChildActive = !this.isChildActive
    }
  }
}
</script>

<style scoped>
.tr {
  position: relative;
  padding-left: 10px;
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
  min-width: 100%;
}

.child-wrapper {
  width: 100%;
}

.child-wrapper .tr {
  border-bottom: none;
  border-right: none;
}

.td {
  padding: 10px;
}

.td.name {
  position: relative;
  padding-left: 20px;
  margin-right: auto;
  border: 1px solid #000;
  border-right: none;
  width: calc(100% - 250px);
}

.td.phone {
  border: 1px solid #000;
  width: 250px;
}

.open-btn {
  padding: 0;
  font-size: 22px;
  line-height: 100%;
  position: absolute;
  left: 3px;
  top: calc(50% - 11px);
  border: none;
  background-color: #fff;
}
</style>
