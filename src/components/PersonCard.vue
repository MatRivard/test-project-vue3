<template>
  <div class="card-wrapper">
    <div
      class="top-img"
      :style="{ backgroundImage: 'url(' + item.bgImg + ')' }"
    >
      <div class="img-hover-content">
        <div>
          <button class="edit">Edit</button>
          <button class="view">View</button>
        </div>
      </div>
    </div>
    <div class="info-container">
      <div class="mobile-wrap">
        <div>
          <h2 class="name">{{ item.name }}</h2>
          <p class="username">@{{ item.username }}</p>
          <p class="catchphrase">"{{ item.company.catchPhrase }}"</p>
        </div>
        <img
          class="mobile-img"
          :src="item.bgImg"
          :alt="'image for ' + item.name"
        />
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> email </span>
        <span class="info-item--text">{{ item.email }}</span>
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> location_on </span>
        <span class="info-item--text">
          {{ item.address.street }},&nbsp;{{ item.address.suite }},
          <br />
          {{ item.address.city }},&nbsp;{{ item.address.zipcode }},
          <br />
          {{ item.address.geo.lat }},&nbsp;{{ item.address.geo.lng }}
        </span>
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> call </span>
        <span class="info-item--text">{{ item.phone }}</span>
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> language </span>
        <span class="info-item--text"
          ><a :href="item.website">{{ item.website }}</a></span
        >
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> business_center </span>
        <span class="info-item--text">{{ item.company.name }}</span>
      </div>
      <div class="info-item">
        <span class="material-icons-outlined"> maps_home_work </span>
        <span class="info-item--text">{{ item.company.bs }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PersonCard",
  props: {
    item: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card-wrapper {
  font-size: 16px;
  color: #202223;
  line-height: 25px;
  text-align: left;
  margin-bottom: 30px;
  max-width: 363px;
  background-color: white;
  border-radius: 8px;
  overflow: hidden;
  word-wrap: break-word;
}
.top-img {
  height: 289px;
  width: 100%;
  background-size: cover;
  background-position: center;
}
.top-img:hover .img-hover-content {
  opacity: 1;
}
.img-hover-content {
  display: flex;
  opacity: 0;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.27);
  height: 100%;
  width: 100%;
  transition: opacity 250ms ease-in-out;
}
.img-hover-content button {
  margin: 0 5px;
  padding: 10px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.img-hover-content .edit {
  background-color: white;
  color: #1575BF;
  border: 1px solid #D2D5D8;
}
.img-hover-content .view {
  background-color: #1575BF;
  color: white;
}
.mobile-img {
  display: none;
}
.info-container {
  padding: 25px 25px 32px;
}
.name,
.username {
  margin: 0;
}
.username {
  color: #909090;
}
.catchphrase {
  margin: 15px 0 21px;
  color: #51C5FF;
}
.material-icons-outlined {
  color: #015989;
}
.info-item {
  display: flex;
  margin: 6px 0;
}
.info-item .info-item--text {
  margin-left: 15px;
  min-width: 0;
}
a {
  color: #202223;
  text-decoration: none;
}
@media screen and (max-width: 700px) {
  .card-wrapper {
    font-size: 13px;
    line-height: 15px;
  }
  .name {
    line-height: 28px;
    font-size: 18px;
  }
  .material-icons-outlined {
    font-size: 14px;
  }
  .top-img {
    display: none;
  }
  .mobile-wrap {
    display: flex;
    justify-content: space-between;
  }
  .mobile-wrap > div {
    margin-right: 20px;
  }
  .mobile-img {
    display: block;
    max-height: 116px;
    border-radius: 8px;
  }
  .card-wrapper {
    max-width: none;
  }
}
</style>
