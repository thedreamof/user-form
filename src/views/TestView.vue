<template>
  <div class="actions">
    <div class="actions-left">
      <div class="info-page">
        <!-- <div class="logo"></div> -->
        <div class="info">
          <div class="subtitle">Todos los</div>
          <div class="title">Beneficiarios</div>
        </div>
      </div>
      <button class="button is-primary" @click="restartForm">+ Nuevo</button>
    </div>

    <div class="actions-right">
      <div class="info-page">
        <!-- <div class="logo"></div> -->
        <div class="info">
          <div class="subtitle">Usuario seleccionado</div>
          <div class="title">Adrian Ortiz Martines</div>
        </div>
      </div>
      <button
        class="button is-primary"
        :class="{ 'is-disabled': formError || !formValidate.isValidate }"
        @click="createUser"
        :disabled="formError || !formValidate.isValidate"
      >
        Guardar
      </button>
      <button
        class="button is-secondary"
        :class="{ 'is-disabled': formError || !formValidate.isValidate }"
        @click="deleteUser"
        :disabled="formError || !formValidate.isValidate"
      >
        - Eliminar
      </button>
    </div>
  </div>

  <div class="content">
    <div class="list">
      <div class="search">
        <input class="input" type="text" placeholder="Buscar" />
      </div>

      <div class="list-card">
        <div
          class="list-item"
          :class="{ active: user.id === userSelected?.id }"
          v-for="user in users"
          :key="user.id"
          @click="editUser(user)"
        >
          <div class="info-page">
            <div class="logo"></div>
            <div class="info">
              <div class="subtitle">Beneficiario</div>
              <div class="title">{{ user.fullName }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="details">
      <div class="user">
        <div class="logo"></div>
        <p>Beneficiario</p>
      </div>
      <div class="form">
        <div class="field">
          <label class="label">
            <span>Nombre completo</span>
            <input
              class="input"
              v-model="form.fullName"
              @blur="validateForm('fullName')"
              type="text"
            />
          </label>
          <span v-if="!formValidate.fullName" class="error">
            Error unicamente se permiten letras y acentos
          </span>
        </div>
        <div class="field">
          <label class="label">
            <span>No. Tarjeta</span>
            <input
              class="input"
              v-model="form.cardNumber"
              @blur="validateForm('cardNumber')"
              type="text"
            />
          </label>
          <span v-if="!formValidate.cardNumber" class="error">
            Error unicamente se permiten números
          </span>
        </div>
        <div class="field">
          <label class="label">
            <span>Saldo</span>
            <input
              class="input"
              v-model.number="form.balance"
              @blur="validateForm('balance')"
              type="text"
            />
            <!-- <input
              class="input"
              :value="userBalance"
              @blur="validateForm('balance')"
              type="text"
              disabled
            /> -->
          </label>
          <span v-if="!formValidate.balance" class="error">
            Error unicamente se permiten números
          </span>
        </div>
        {{ userBalance }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { ref } from 'vue';
import type { UserI } from '@/interfaces/user';
import userMock from '@/mock/user';

// --- Variables
const users = ref<Array<UserI>>([]);
const userSelected = ref<UserI>();
const form = ref<UserI>({
  id: '',
  fullName: '',
  cardNumber: null,
  balance: null,
});

const formValidate = ref<any>({
  isValidate: false,
  fullName: true,
  cardNumber: true,
  balance: true,
});

const formError = computed(() => {
  if (
    !formValidate.value.fullName ||
    !formValidate.value.cardNumber ||
    !formValidate.value.balance
  ) {
    return true;
  }
  return false;
});

const validateForm = (field = '') => {
  formValidate.value.isValidate = true;
  const regex = /^[\sa-zA-Z\u00C0-\u017F]+$/; // espacios, letras y acentos
  switch (field) {
    case 'fullName':
      formValidate.value[field] = !!form.value.fullName.match(regex)?.length;
      break;
    case 'cardNumber':
      formValidate.value[field] = Number(form.value.cardNumber);
      break;
    case 'balance':
      formValidate.value[field] = Number(form.value.balance);
      break;
    default:
      formValidate.value.fullName = !!form.value.fullName.match(regex)?.length;
      formValidate.value.cardNumber = Number(form.value.cardNumber);
      formValidate.value.balance = Number(form.value.balance);
      break;
  }
};

// --- functions
const userBalance = computed(() =>
  form.value.balance?.toLocaleString('en-US', { minimumFractionDigits: 2 })
);

const generateId = () =>
  Math.floor(Math.random() * (100000 - 1000 + 1) + 1000).toString();

const resetForm = () => {
  form.value.id = '';
  form.value.fullName = '';
  form.value.cardNumber = null;
  form.value.balance = null;
};

const resetFormValidation = () => {
  formValidate.value.isValidate = false;
  formValidate.value.fullName = true;
  formValidate.value.cardNumber = true;
  formValidate.value.balance = true;
};

const deleteRepeated = (data: Array<any>) => {
  data = data.filter((item, index) => {
    return data.findIndex((element) => element.id === item.id) === index;
  });
  return data;
};

const getUserTemp = () => {
  const usersSaved = JSON.parse(localStorage.getItem('users') || '[]');
  users.value = [...userMock, ...usersSaved];
  users.value = deleteRepeated(users.value);
};

const getUsers = () => {
  const usersSaved = JSON.parse(localStorage.getItem('users') || '[]');
  users.value = [...usersSaved];
};

const restartForm = () => {
  userSelected.value = undefined;
  resetForm();
  resetFormValidation();
};

const createUser = () => {
  const user = { ...form.value };

  if (!userSelected.value?.id) {
    // --- Create
    user.id = generateId();
    users.value.push(user);
    localStorage.setItem('users', JSON.stringify(users.value));
  } else {
    // --- Edit
    users.value = users.value.map((x) => {
      if (x.id === user.id) return user;
      return x;
    });
  }

  localStorage.setItem('users', JSON.stringify(users.value));
  restartForm();
  getUsers();
};

const editUser = (user: UserI) => {
  userSelected.value = user;
  form.value = { ...user };
  validateForm();
};

const deleteUser = () => {
  users.value = users.value.filter(
    (user) => user.id !== userSelected.value?.id
  );
  localStorage.setItem('users', JSON.stringify(users.value));
  restartForm();
  getUsers();
};

// --- Initialized functions
getUserTemp();
</script>

<style scoped lang="scss">
.actions {
  height: 80px;
  width: 100%;
  background: var(--background-1);
  border: 1px solid var(--background-2);
  display: flex;
  align-items: center;
}

.content {
  display: flex;
  height: 100%;
}
.list {
  min-width: 300px;
  height: 100%;
  background: var(--background-2);
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
}

// --- to refactor
.info-page {
  display: flex;
  align-items: center;
  width: 100%;
  margin-left: 15px;
}

.subtitle {
  color: var(--text-light);
  font-size: 0.9rem;
}

.title {
  font-weight: bold;
  font-size: 1rem;
}

.logo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
  background: var(--background-3);
}

.actions-left {
  display: flex;
  min-width: 300px;
  padding-right: 10px;
}

.actions-right {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.input {
  padding: 5px;
  border-radius: 5px;
  background: var(--background-3);
  border: 1px solid #d3d3d3;
  padding: 10px;
  width: 100%;
}

.search {
  width: 90%;
  margin: 10px 0;
  .input {
    padding: 5px;
    border-radius: 5px;
    background: #eaebeb;
    border: 1px solid #d3d3d3;
    padding: 10px;
    width: 100%;

    &::placeholder {
      color: black;
      font-weight: bold;
    }
  }
}

.list-card {
  width: 90%;
  height: 100%;
}

.list-item {
  padding: 5px;
  background: var(--background-1);
  border-radius: 8px;
  margin-bottom: 10px;
  // border-radius: 20px;

  .logo {
    height: 40px;
    width: 40px;
  }

  .title {
    font-size: 1rem;
  }

  .subtitle {
    font-size: 0.8rem;
  }

  &.active {
    border: 2px solid var(--primary);
    color: var(--primary);
    .logo {
      background: var(--primary);
    }
  }

  &:hover {
    cursor: pointer;
    background: var(--background-4);
    border: 1px solid var(--primary);
    color: var(--primary);
  }
}

// ---- Details -------------------------------
.details {
  width: 100%;
  height: 100%;
  margin-top: 50px;
  display: flex;
}

.user {
  width: 20%;
  border-right: 1px solid var(--background-2);
  display: flex;
  flex-direction: column;
  align-items: center;

  .logo {
    width: 100px;
    height: 100px;
    margin-bottom: 20px;
  }

  p {
    color: var(--text-light);
  }
}

.form {
  padding: 0 15px;
  width: 100%;
}

.field {
  margin: 15px 0;

  .error {
    font-size: 0.8rem;
    color: var(--secondary);
  }
}

.label {
  color: var(--text-light);
  font-size: 0.8rem;
}
</style>
