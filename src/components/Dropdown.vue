<template>
  <div class="dropdown-wrapper">
    <button class="filter-dropdown" v-on:click="toggleDropdown">
      <span>Filter by&nbsp;{{ selected }}</span>
      <span v-if="menuIsOpen" class="material-icons-outlined">
        arrow_drop_up
      </span>
      <span v-else class="material-icons-outlined"> arrow_drop_down </span>
    </button>
    <div v-if="menuIsOpen" class="dropdown-content">
      <ul class="dropdown-list">
        <li
          v-for="(option, index) of options"
          :key="index"
          v-on:click="selectOption(option)"
          class="dropdown-item"
        >
          {{ option }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dropdown",
  data() {
    return {
      menuIsOpen: false,
      selected: null,
      options: ["Name (A-Z)", "Name (Z-A)"],
    };
  },
  methods: {
    toggleDropdown: function () {
      this.menuIsOpen = !this.menuIsOpen;
    },
    selectOption: function (option) {
      if (this.selected !== option) {
        this.selected = option;
        this.$emit("dropdown-select", this.selected);
      }
      this.toggleDropdown();
    },
  },
};
</script>

<style scoped>
.filter-dropdown {
  border: none;
  cursor: pointer;
  min-width: 222px;
  padding: 15px 17px;
  font-size: 16px;
  border-radius: 8px;
  background-color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.filter-dropdown option {
  height: 50px;
}
.dropdown-wrapper {
  position: relative;
}
.dropdown-content {
  position: absolute;
  top: calc(100% + 4px);
  border-radius: 4px;
  background: white;
  width: 100%;
  z-index: 100;
}
.dropdown-list {
  list-style: none;
  padding: 8px 10px;
  margin: 0;
}
.dropdown-item {
  padding: 15px 8px;
  border-radius: 4px;
  line-height: 25px;
  font-size: 16px;
  cursor: pointer;
}

.dropdown-item:hover {
  background-color: #F6F6F7;
}
</style>