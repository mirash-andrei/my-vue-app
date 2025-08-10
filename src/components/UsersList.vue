<script setup>
import { ref } from "vue";
import logo from "../assets/logo-user.png";

const users = [
  {
    id: 1,
    name: "Иванов Иван Иванович",
    position: "Руководитель отдела",
    department: "Отдел продаж",
    mail: "ivanovII@ya.ru",
    phone: "+7(999)111-00-01",
  },
  {
    id: 2,
    name: "Петров Петр Сергеевич",
    position: "Логист",
    department: "Отдел логистики",
    mail: "PetrovPS@ya.ru",
    phone: "+7(999)222-00-01",
  },
  {
    id: 3,
    name: "Сидоров Сергей Михайлович",
    position: "Главный бухгалтер",
    department: "Бухгалтерия",
    mail: "sidorovSM@ya.ru",
    phone: "+7(999)333-00-01",
  },
];

const showUsersList = ref();
const contactsState = ref({});
const btnColor = ref("#000000");

function toggleUserList() {
  showUsersList.value = !showUsersList.value;
}

function toggleContacts(userId) {
  contactsState.value[userId] = !contactsState.value[userId];
}
</script>

<template>
  <h1>Список пользователей</h1>
  <div class="select-color">
    <label for="select-color">Выберите цвет текста кнопки при наведении</label>
    <input id="select-color" type="text" v-model="btnColor" />
  </div>
  <button @click="toggleUserList" class="btn">
    {{ showUsersList ? "Скрыть" : "Показать" }} список пользователей
  </button>
  <div v-if="showUsersList" class="user-list">
    <div class="user-card" v-for="user in users" :key="user.id">
      <div class="user-card-logo">
        <img :src="logo" alt="logo" />
      </div>
      <div class="user-card-description">
        <h2>{{ user.name }}</h2>
        <p>{{ user.position }}</p>
        <p>{{ user.department }}</p>
        <button class="btn" @click="toggleContacts(user.id)">
          {{ contactsState[user.id] ? "Скрыть контакты" : "Показать контакты" }}
        </button>
        <div v-if="contactsState[user.id]" class="contacts">
          <p>{{ user.mail }}</p>
          <p>{{ user.phone }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.select-color {
  margin: 20px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  label {
    margin-bottom: 8px;
  }
  input {
    height: 24px;
    width: 380px;
    border-radius: 8px;
    padding: 4px 8px;
    border: 1px solid #aaaaaa;
    &:focus {
      outline: none;
    }
  }
}
.user {
  &-list {
    display: flex;
    flex-direction: column;
    margin: 20px 0;
  }
  &-card {
    display: flex;
    background: white;
    padding: 10px;
    border-radius: 15px;
    margin-bottom: 10px;
    &-logo {
      display: flex;
      height: 100px;
      padding-right: 10px;
    }
    &-description {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      .contacts {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
      }
    }
  }
}
.btn {
  background: #aaaaaa;
  padding: 12px 24px;
  border-radius: 8px;
  transition: 0.3s ease;
  &:hover {
    background: #c7c7c7;
    color: v-bind("btnColor");
  }
}
</style>
