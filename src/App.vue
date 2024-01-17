<template>
  <div id="app">
    <h1>CRUD Simple con Vue.js</h1>
    <div>
      <input v-model="newItem" @keyup.enter="addItem" />
      <button @click="addItem">Añadir</button>
    </div>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <template v-if="editIndex === index">
          <input
            :value="item"
            @input="(event) => editItem(index, event.target.value)"
          />
          <button @click="updateItem()">Guardar</button>
          <button @click="cancelEdit">Cancelar</button>
        </template>
        <template v-else>
          {{ item }}
          <button @click="enableEdit(index)">Editar</button>
          <button @click="deleteItem(index)">Eliminar</button>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      newItem: "",
      items: [],
      editIndex: -1, // Índice del ítem que se está editando, -1 significa que no se está editando nada
    };
  },
  methods: {
    addItem() {
      if (this.newItem.trim() !== "") {
        this.items.push(this.newItem);
        this.newItem = "";
      }
    },
    editItem(index, value) {
      this.items[index] = value;
      this.items = [...this.items];

    },
    updateItem() {
      this.editIndex = -1; // Salir del modo de edición
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
    enableEdit(index) {
      this.editIndex = index; // Entrar en modo de edición para este ítem
    },
    cancelEdit() {
      this.editIndex = -1; // Cancelar la edición
    },
  },
};
</script>
<style>
#app {
  max-width: 500px;
  margin: 40px auto;
  padding: 20px;
  border: 1px solid #e1e1e1;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background: #fff;
  font-family: 'Helvetica Neue', Arial, sans-serif;
}

h1 {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1.5rem;
}

div > input[type="text"] {
  width: calc(100% - 100px);
  margin-right: 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.9rem;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

button:hover {
  opacity: 0.8;
}

button:active {
  transform: scale(0.98);
}

/* Colores específicos para botones */
.add-btn {
  background-color: #5cb85c;
  color: #fff;
}

.edit-btn {
  background-color: #f0ad4e;
  color: #fff;
}

.delete-btn {
  background-color: #d9534f;
  color: #fff;
}

.save-btn {
  background-color: #5bc0de;
  color: #fff;
}

.cancel-btn {
  background-color: #999;
  color: #fff;
}

ul {
  padding-left: 0;
  list-style-type: none;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
  padding: 10px;
  background: #f9f9f9;
  border: 1px solid #e1e1e1;
  border-radius: 4px;
}

li:not(:first-child) {
  margin-top: 15px;
}

li input[type="text"] {
  flex-grow: 1;
  margin-right: 10px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

li .edit-buttons {
  display: flex;
  gap: 10px;
}

/* Mejorar la visualización en dispositivos móviles */
@media (max-width: 768px) {
  #app {
    width: 90%;
    margin: 20px auto;
  }

  div > input[type="text"] {
    width: calc(100% - 80px);
  }

  button {
    padding: 8px 12px;
  }
}
</style>
