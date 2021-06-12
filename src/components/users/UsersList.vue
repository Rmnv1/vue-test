<template>
  <div>
    <h1>Список пользователей</h1>
    <div class="table-wrap">
      <table class="table">
        <thead>
          <tr>
            <th @click="sortUsers">
              Имя
              <img
                src="@/assets/icons/arrow.svg"
                alt="Sort arrow icon"
                class="table__sort-arrow"
                :class="{sortIconRotate: !listSorted}"
              />
            </th>
            <th>
              Телефон
            </th>
          </tr>
        </thead>
        <tbody v-for="person in usersList" :key="person.name + '_' + person.phone">
          <tr>
            <td>{{person.name}}</td>
            <td>{{person.phone}}</td>
          </tr>
          <tr v-for="person in person.staff" :key="person.name + '_' + person.phone" class="child-row">
            <td>
              <img src="@/assets/icons/child-arrow.svg" alt="Child arrow" class="child-row__icon">
              {{person.name}}
            </td>
            <td>{{person.phone}}</td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      listSorted: false
    }
  },
  props: ['usersList'],
  methods: {
    sortUsers() {
      if (!this.listSorted) {
        this.usersList.sort((a, b) => a.name.localeCompare(b.name));
      } else {
        this.usersList.sort((a, b) => b.name.localeCompare(a.name));
      }
      this.listSorted = !this.listSorted;
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.table-wrap {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
}
.table {
  width: 100%;
  max-width: 600px;
  border-collapse: collapse;
  margin-bottom: 30px;
  & th {
    padding: 8px;
    cursor: pointer;
  }
  & td {
    padding: 8px;
  }
  & tr {
    border-top: 1px solid #e0e0e0;
    text-align: left;
    position: relative;
    transform: translateX(18%);
  }
}
.child-row {
  position: relative;
  left: 15px;
}
.child-row__icon {
  max-width: 12px;
  max-height: 12px;
  transform: rotateY(180deg);
}

.table__sort-arrow {
  display: inline-block;
  max-width: 10px;
  max-height: 10px;
  position: relative;
  margin-left: 3px;
}
.sortIconRotate{
  transition: .2s all;
  transform: rotate(180deg);
}
@media screen and (max-width: 480px) {
  .table tr{
    transform: translateX(10%);
  }
}
</style>
