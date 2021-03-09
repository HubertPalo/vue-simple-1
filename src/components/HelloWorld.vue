<template>
  <!--<ul id="example-1">
    <li v-for="item in list" :key="item">
      {{ item }}
    </li>
  </ul>-->
  <div class="container">
    <div class="block" v-for="item in list" :key="item.id">
      <div
        class="card has-background-link-light"
        @click="
          triggerModal();
          selectItem(item);
        "
      >
        <div class="card-content">
          <div class="content">
            <p>
              <b>{{ item.attributes.titles.en_jp }}</b> [JP:{{
                item.attributes.titles.ja_jp
              }}]
            </p>
          </div>
        </div>
      </div>
    </div>
    <div
      class="modal"
      v-bind:class="{ 'is-active': showModal }"
      v-if="selectedItem"
    >
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">
            <b>{{ selectedItem.attributes.titles.en_jp }}</b>
          </p>
        </header>
        <section class="modal-card-body">
          <p class="image is-4by3">
            <img
              :src="selectedItem.attributes.posterImage.medium"
              alt=""
            />
          </p>
          <p>{{ selectedItem.attributes.synopsis }}</p>
        </section>
      </div>
      <button
        class="modal-close is-large"
        aria-label="close"
        @click="triggerModal"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: function () {
    return {
      list: [],
      showModal: false,
      selectedItem: null,
    };
  },
  methods: {
    triggerModal() {
      this.showModal = !this.showModal;
    },
    selectItem(newItem) {
      this.selectedItem = newItem;
    },
  },
  mounted() {
    this.$http
      .get("https://kitsu.io/api/edge/anime")
      .then((response) => (this.list = response.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
