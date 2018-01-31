<template>
  <div class='col-md-4' @click="switchItem">
    <div class="item-card">
      <div class="card-block">
        <h4 class="card-title">{{propitem.name}}</h4>
        <div
        v-for="(value, key, index) in propitem"
        :key="key">
          <div v-if="index<5">
            <strong>{{key}}</strong>:{{value}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item", "type"],
  // props: ["passedItem", "type"],
  data() {
    return { propitem: this.item };
  },
  methods: {
    switchItem() {
      let random_id = Math.floor(Math.random() * 63) + 1;
      fetch(`https://swapi.co/api/${this.type}/${random_id}`, {
        method: "GET"
      })
        .then(res => res.json())
        .then(json => (this.propitem = json));
    }
  }
};
</script>
