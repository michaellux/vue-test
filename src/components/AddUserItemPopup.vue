<template>
<div id="popup" class="overlay">
  <div class="popup">
    <h2>Добавление пользователя</h2>
    <a class="close" href="#">&times;</a>
    <div class="content">
      <form>
        <div class="form-block">
          <label for="name">Имя</label>
          <input required v-model="potentialUser.name"
          class="input-name" name="name" id="name" type="text">
        </div>
        <div class="form-block">
          <label for="phone">Телефон</label>
          <input required
          v-model="potentialUser.phone" class="input-phone" name="phone" id="phone" type="tel">
        </div>
        <div class="form-block">
          <label for="boss">Начальник</label>
          <select v-model="potentialUser.boss" class="select-boss" name="boss" id="boss">
            <option value="">Нет начальника</option>
            <option
            v-for="potentialBoss in potentialBosses"
            :key="potentialBoss.id" :value="potentialBoss.id">{{potentialBoss.name}}</option>
          </select>
        </div>
        <p v-if="hasValidationFormErrors">
          <b>Пожалуйста, проверьте введённую информацию.</b>
          <ul>
              <li
                v-for="validationError in validationErrors"
                :key="validationError.id">{{ validationError.name }}</li>
          </ul>
        </p>
        <input type="button" @click="handleFormData" class="save-button" value="Сохранить">
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
      defaultSelect: 'Нет начальника',
      potentialUser: {
        name: '',
        phone: '',
        boss: null,
      },
      validationErrors: [],
    };
  },
  methods: {
    handleFormData() {
      this.clearValidationErrors();
      if (this.checkFormForValidData()) {
        this.addUser();
      }
    },
    addUser() {
      const users = this.$parent.users;
      const allUserIds = users.map(user => user.id);
      const maxUserId = Math.max(...allUserIds);
      const user = {
        id: maxUserId + 1,
        name: this.potentialUser.name,
        phone: this.potentialUser.phone,
        parent: this.potentialUser.boss === '' ? null : this.potentialUser.boss,
      };

      const updatedUserList = [...this.$parent.users, user];
      updatedUserList.forEach((element, index) => {
        this.$set(this.$parent.users, index, element);
      });

      this.saveUser();
    },
    saveUser() {
      const users = this.$parent.users;
      const parsedUsers = JSON.stringify(users);
      localStorage.setItem('users', parsedUsers);
    },
    checkFormForValidData() {
      this.defineValidationErrors();

      if (this.hasValidationFormErrors) {
        return false;
      }
      return true;
    },
    clearValidationErrors() {
      this.validationErrors = [];
    },
    defineValidationErrors() {
      if (this.potentialUser.name === '') {
        const validationNameError = { id: 1, name: 'Не указано имя' };
        this.validationErrors = [...this.validationErrors, validationNameError];
      }
      if (this.СheckforWrongSymbolsInPhoneNumber(this.potentialUser.phone)) {
        const validationSymbolsPhoneError = { id: 2, name: 'Неправильно указан телефон' };
        this.validationErrors = [...this.validationErrors, validationSymbolsPhoneError];
      }
    },
    СheckforWrongSymbolsInPhoneNumber(dataForCheck) {
      const re = /^[0-9() -]+$/;
      if (!re.test(dataForCheck)) {
        return true;
      }
      return false;
    },
  },
  computed: {
    potentialBosses() {
      const potentialBosses = this.$parent.users;
      return potentialBosses;
    },
    hasValidationFormErrors() {
      return this.validationErrors.length > 0;
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
  font-size: 1rem;
}

.popup .close {
  position: absolute;
  top: 10px;
  right: 20px;
  -webkit-transition: all 200ms;
  transition: all 200ms;
  font-size: 1.5rem;
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
  flex-wrap: wrap;
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

@media screen and (max-width: 1000px){
  .popup{
    width: 70%;
  }
}
</style>
