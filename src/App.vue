<template>
  <div id="app">
    <UsersList :usersList="usersList" />
    <AddUser :addNewUser="addNewUser" :listOfChiefs="listOfChiefs" />
  </div>
</template>

<script>
import UsersList from "@/components/users/UsersList.vue";
import AddUser from "@/components/users/AddUser.vue";

export default {
  name: "App",
  data() {
    return {
      usersList: [
        {
          name: "Марина",
          phone: "+7 (999) 999-99-99",
          staff: [
            {
              name: "Григорий",
              phone: "+7 (999) 999-99-99",
            },
          ],
        },
        {
          name: "Пётр",
          phone: "+7 (999) 999-99-99",
          staff: [],
        },
        {
          name: "Алексей",
          phone: "+7 (999) 999-99-99",
          staff: [
            {
              name: "Иван",
              phone: "+7 (999) 999-99-99",
            },
          ],
        },
        {
          name: "Борис",
          phone: "+7 (999) 999-99-99",
          staff: [],
        },
      ],
      listOfChiefs: ["Марина", "Пётр", "Алексей", "Борис"],
    };
  },
  components: {
    UsersList,
    AddUser,
  },
  methods: {
    addNewUser(newUserData) {
      // Check chief field
      if (newUserData.chief) {
        this.usersList.forEach((elem) => {
          if (newUserData.chief == elem.name) {
            elem.staff.push({
              name: newUserData.name,
              phone: newUserData.phone,
            });
          }
        });
      } else {
        this.usersList.push({
          name: newUserData.name,
          phone: newUserData.phone,
          staff: []
        })
        this.listOfChiefs.push(newUserData.name);
      }
      this.saveUsersToLocal()
    },
    saveUsersToLocal() {
      // Save list of users to local storage
      window.localStorage.setItem('usersList', JSON.stringify(this.usersList));
      // Save list of chiefs to local storage
      window.localStorage.setItem('listOfChiefs', JSON.stringify(this.listOfChiefs));
    },
    loadUsersFromLocal() {
      // Load list of users from local storage
      this.usersList = JSON.parse(window.localStorage.getItem('usersList')) || this.usersList;
      // Load list of chiefs from local storage
      this.listOfChiefs = JSON.parse(window.localStorage.getItem('listOfChiefs')) || this.listOfChiefs;
    }
  },
  mounted() {
    this.loadUsersFromLocal()
  }
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
html {
  height: 100%;
}
body {
  background: linear-gradient(to top, #ddecff, #fff);
  position: relative;
  width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  overflow: hidden;
  padding: 0 10px;
}

.btn {
  display: flex;
  justify-content: center;
  background: #2589ff;
  border-radius: 6px;
  padding: 12px 30px;
  font-size: 16px;
  line-height: 20px;
  color: #ffffff;
  cursor: pointer;
  border: 0;
  transition: 0.2s all;
  &:hover {
    background: lighten($color: #2589ff, $amount: 5%);
  }

  // modifiers
  &--center {
    margin-left: auto;
    margin-right: auto;
  }
  &--modal {
    margin-top: 25px;
  }
}
</style>
