<template>
<div id="popup" class="overlay">
  <div class="popup">
    <h2>Добавление пользователя</h2>
    <a class="close" href="#">&times;</a>
    <div class="content">
      <form>
        <div class="form-block">
          <label for="name">Имя</label>
          <input required v-model="newUser.name"
          class="input-name" name="name" id="name" type="text">
        </div>
        <div class="form-block">
          <label for="phone">Телефон</label>
          <input required
          v-model="newUser.phone" class="input-phone" name="phone" id="phone" type="tel">
        </div>
        <div class="form-block">
          <label for="boss">Начальник</label>
          <select v-model="newUser.boss" class="select-boss" name="boss" id="boss">
            <option value="">Нет начальника</option>
            <option v-for="boss in bosses" :key="boss.id" :value="boss.id">{{boss.name}}</option>
          </select>
        </div>
        <button type="button" @click="addUser"
        class="save-button">Сохранить</button>
      </form>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'AddUserItemPopup',
  props: {
    users: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      newUser: {
        name: '',
        phone: '',
        boss: null,
      },
    };
  },
  methods: {
    addUser() {
      const users = this.$parent.users;
      const allUserIds = users.map(user => user.id);
      const maxUserId = Math.max(...allUserIds);
      const user = {
        id: maxUserId + 1,
        name: this.newUser.name,
        phone: this.newUser.phone,
        parent: this.newUser.boss === '' ? null : this.newUser.boss,
      };

      const updatedUserList = [...this.$parent.users, user];
      updatedUserList.forEach((element, index) => {
        this.$set(this.$parent.users, index, element);
      });
    },
  },
  computed: {
    bosses() {
      const users = this.$parent.users;
      const employees = users.filter(user => user.parent !== null);
      const bossesId = employees.map(employee => employee.parent);
      const bosses = users.filter(user => bossesId.includes(user.id));
      return bosses;
    },
  },
};
</script>

<style>
.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
}

.overlay:target {
  visibility: visible;
  opacity: 1;
}

.popup {
  margin: 70px auto;
  padding: 20px;
  background: #fff;
  border-radius: 5px;
  width: 30%;
  position: relative;
  transition: all 5s ease-in-out;
}

.popup h2 {
  margin-top: 0;
  color: #333;
  font-family: Tahoma, Arial, sans-serif;
}

.popup .close {
  position: absolute;
  top: 20px;
  right: 30px;
  transition: all 200ms;
  font-size: 30px;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}

.popup .close:hover {
  color: #06D85F;
}

.popup .content {
  max-height: 30%;
  overflow: auto;
}

.form-block {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 2rem;
}

.save-button {
    background-color: #3e2ac0;
    border: none;
    color: white;
    padding: 1rem 2rem;
    border-radius: 2rem;
    text-decoration: none;
    font-size: 16px;
    margin: 2rem;
    float: left;
}

.input-name, .input-phone {
  padding: 0.3rem 0;
}

.select-boss {
  width: 40%;
  padding: 0.3rem 0;
}

@media screen and (max-width: 700px){
  .popup{
    width: 70%;
  }
}
</style>
