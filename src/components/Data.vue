<template>
  <div class="col-md-12 itemConatiner">
   <Item
   v-for="(item, i) in items"
   :key="i"
   :item="item"
   :type="type"
   />
  </div>
</template>

<script>
import Item from "./Item";
export default {
  data() {
    return {
      type: this.$route.params.type,
      items: []
    };
  },
  watch: {
    $route: "fetchItems"
  },
  methods: {
    fetchItems() {
      this.items = [];
      this.type = this.$route.params.type;
      let initial_ids = [1, 13, 16];
      for (let i in initial_ids) {
        let id = initial_ids[i];
        fetch(`https://swapi.co/api/${this.type}/${id}`, { method: "GET" })
          .then(res => res.json())
          // json => every character info
          .then(json => this.items.push(json));
      }
    }
  },
  created() {
    this.fetchItems();
  },
  components: { Item }
};
</script>

