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
      <button class="button is-primary">+Nuevo</button>
    </div>

    <div class="actions-right">
      <div class="info-page">
        <!-- <div class="logo"></div> -->
        <div class="info">
          <div class="subtitle">Usuario seleccionado</div>
          <div class="title">Adrian Ortiz Martines</div>
        </div>
      </div>
      <button class="button is-primary">Guardar</button>
      <button class="button is-secondary">-Eliminar</button>
    </div>
  </div>

  <div class="content">
    <div class="list">
      <div class="search">
        <input class="input" type="text" placeholder="Buscar" />
      </div>

      <div class="list-card">
        <div class="list-item active">
          <div class="info-page">
            <div class="logo"></div>
            <div class="info">
              <div class="subtitle">Beneficiario</div>
              <div class="title">Adrian Ortiz Martines</div>
            </div>
          </div>
        </div>

        <div class="list-item">
          <div class="info-page">
            <div class="logo"></div>
            <div class="info">
              <div class="subtitle">Beneficiario</div>
              <div class="title">Adrian Ortiz Martines</div>
            </div>
          </div>
        </div>

        <div class="list-item">
          <div class="info-page">
            <div class="logo"></div>
            <div class="info">
              <div class="subtitle">Beneficiario</div>
              <div class="title">Adrian Ortiz Martines</div>
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
            <span> Nombre completo</span>
            <input class="input" type="text" />
          </label>
        </div>
        <div class="field">
          <label class="label">
            <span> No. Tarjeta</span>
            <input class="input" type="number" />
          </label>
        </div>
        <div class="field">
          <label class="label">
            <span> Saldo</span>
            <input
              class="input"
              type="number"
              min="0.00"
              max="10000.00"
              step="0.01"
            />
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts"></script>

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
}

.label {
  color: var(--text-light);
  font-size: 0.8rem;
}
</style>
