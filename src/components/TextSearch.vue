<template>
  <div class="name-filter">
    <input
      v-on:input="$emit('filter-text', $event.target.value)"
      class="name-filter--input"
      placeholder="Find customers"
    />
    <span class="material-icons-outlined search"> search </span>
  </div>
</template>

<script>
export default {
  name: "TextSearch",
};
</script>

<style scoped>
.search {
  position: absolute;
  left: 22px;
  font-size: 16px;
  top: calc(50% - 8px);
}
.name-filter {
  position: relative;
  width: 100%;
}
.name-filter input {
  padding: 15px 5px 15px 48px;
  width: 546px;
  font-size: 16px;
  border-radius: 8px;
  line-height: 20px;
  border: none;
}
.name-filter input::placeholder {
  color: #202223;
  line-height: normal !important;
}
@media screen and (max-width: 950px) {
  .name-filter input {
    width: 350px;
  }
}
@media screen and (max-width: 700px) {
  .name-filter {
    margin-bottom: 34px;
  }
  .name-filter input {
    width: -webkit-fill-available;
  }
}
</style>