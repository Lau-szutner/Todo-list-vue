<template>
  <div
    class="container d-flex flex-column align-items-center mt-5"
    @keyup.enter="keyEnter"
  >
    <h1>Todo List</h1>
    <p>Total tasks {{ totalItems }}</p>

    <div id="listContainer" class="rounded-3 p-4 w-75">
      <form
        action=""
        class="d-flex gap-3 align-items-center flex-column flex-md-row"
      >
        <textarea
          name=""
          v-model="input"
          value="text"
          class="text-black col-12 col-md-9"
        ></textarea>
        <button
          @click.prevent="add"
          id="addButton"
          class="p-3 border-0 rounded-2 col-12 col-md-3"
        >
          Add
        </button>
      </form>
      <ul class="px-0 d-flex flex-column gap-1 my-2" v-if="hasItem">
        <li
          v-for="(item, index) in tasks"
          class="todoItem d-flex align-center justify-content-between p-2 px-4 rounded-1"
          :key="index"
          :class="{ completed: item.completed, delete: item.delete }"
        >
          <p class="text-white d-flex align-items-center mb-0">
            {{ item.name }}
          </p>
          <div class="d-flex gap-2">
            <button
              class="border-0 rounded-1 check-button"
              @click.prevent="completedT(index)"
              v-if="item.completed === false"
            >
              <img
                src="./assets/check2.svg"
                alt="Ejemplo SVG"
                class="border-0 p-2"
              />
            </button>

            <button
              class="border-0 rounded-1 delete-button"
              @click.prevent="del(index)"
              v-else-if="item.delete === false"
            >
              <img
                src="./assets/trash3.svg"
                alt="Ejemplo SVG"
                class="border-0 p-2"
              />
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      hasItem: null,
      tasks: [],
      input: "",
      isHover: [],
      completed: false,
      beDelete: false,
    };
  },
  computed: {
    totalItems() {
      if (this.tasks.length >= 1) {
        this.hasItem = true;

        return this.tasks.length;
      } else {
        this.hasItem = false;
        return this.tasks.length;
      }
    },
  },
  methods: {
    add() {
      if (this.input.trim() === "") {
        return;
      } else {
        this.tasks.unshift({
          name: this.input,
          completed: this.completed,
          delete: this.beDelete,
        });
        this.input = "";
      }
    },
    keyEnter() {
      this.add();
    },
    completedT(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    del(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
#listContainer {
  background-color: var(--bg-color-container);
}

#addButton {
  background-color: #41b883;
}

.todoItem {
  background-color: #3f3f3f;
}

button img {
  width: 40px;
}

.hover-color {
  filter: invert(100%) sepia(10%) saturate(2041%) hue-rotate(265deg)
    brightness(114%) contrast(92%);
}

.delete-button:hover {
  background-color: rgb(255, 0, 0);
  img {
    filter: invert(100%) sepia(10%) saturate(2041%) hue-rotate(265deg)
      brightness(114%) contrast(92%);
  }
}

.check-button:hover {
  background-color: #41b883;
  img {
    filter: invert(100%) sepia(10%) saturate(2041%) hue-rotate(265deg)
      brightness(114%) contrast(92%);
  }
}

.completed {
  background-color: #41b8839c;
}

.delete {
  background-color: red;
}
</style>
