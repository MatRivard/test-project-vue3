<template>
  <div id="content-outer">
    <div class="top-bar"></div>
    <div id="content-inner">
      <div class="filters">
        <TextSearch v-on:filter-text="searchString = $event" />
        <Dropdown v-on:dropdown-select="sortCustomers($event)" />
      </div>
      <div id="person-grid">
        <PersonCard
          v-for="(item, index) in filteredItems"
          :key="index"
          :item="item"
        />
        <div v-if="filteredItems.length === 0" class="not-found-text">
          No customers found for "{{ searchString }}".
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PersonCard from "./components/PersonCard";
import Dropdown from "./components/Dropdown";
import TextSearch from "./components/TextSearch";
import faker from "faker";

export default {
  name: "App",
  components: {
    PersonCard,
    Dropdown,
    TextSearch,
  },
  data() {
    return {
      items: [],
      searchString: "",
    };
  },
  methods: {
    fetchData() {
      fetch("https://jsonplaceholder.typicode.com/users")
        .then((response) => response.json())
        .then((json) => {
          // Fake profile image generated with faker since API didn't contain images
          // Also capitalized first letter of company.bs to match mock up
          json.forEach((item) => {
            item.bgImg = faker.image.avatar();
            item.company.bs =
              item.company.bs.charAt(0).toUpperCase() +
              item.company.bs.slice(1);
          });
          this.items = json;
        });
    },
    sortCustomers(sortOrder) {
      const sortAscend = (a, b) =>
        a.name < b.name ? -1 : a.name > b.name ? 1 : 0;
      const sortDescend = (a, b) => -sortAscend(a, b);
      this.items.sort(sortOrder === "Name (A-Z)" ? sortAscend : sortDescend);
    },
  },
  computed: {
    filteredItems: function () {
      return this.items.filter((item) => {
        return item.name
          .toLowerCase()
          .includes(this.searchString.toLowerCase());
      });
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style>
* {
  font-family: "Rubik", sans-serif;
}
body {
  margin: 0;
}
#content-outer {
  background-color: #E5E5E5;
  min-height: 100vh;
}
#content-inner {
  max-width: 1650px;
  margin: 0 auto;
  padding: 80px 40px 0;
  font-size: 16px;
  position: relative;
}
.top-bar {
  width: 100%;
  height: 65px;
  background-color: white;
  box-shadow: 9px 6px 24px -2px rgba(0, 0, 0, 0.06);
}
.filters {
  display: flex;
  justify-content: space-between;
}

#person-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  padding-top: 100px;
  grid-column-gap: 40px;
  justify-content: space-between;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.not-found-text {
  text-align: center;
}
@media screen and (max-width: 1300px) {
  #person-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
@media screen and (max-width: 950px) {
  #person-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media screen and (max-width: 700px) {
  #content-inner {
    padding: 26px 23px;
  }
  #person-grid {
    display: block;
  }
  .filters {
    flex-direction: column;
    align-items: flex-end;
  }
}
</style>
