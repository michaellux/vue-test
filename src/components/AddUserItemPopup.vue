<template>
<div id="popup" class="overlay">
  <div class="popup">
    <h2>Добавление пользователя</h2>
    <a class="close" href="#">&times;</a>
    <div class="content">
      <form>
        <div class="form-block">
          <label for="name">Имя</label>
          <input class="input-name" name="name" id="name" type="text">
        </div>
        <div class="form-block">
          <label for="phone">Телефон</label>
          <input class="input-phone" name="phone" id="phone" type="tel">
        </div>
        <div class="form-block">
          <label for="boss">Начальник</label>
          <select class="select-boss" name="boss" id="boss">
            <option disabled value="">Test</option>
          </select>
        </div>
        <a class="save-button" href="#popup">Сохранить</a>
      </form>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'AddUserItemPopup',
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
