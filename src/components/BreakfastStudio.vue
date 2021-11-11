<template>
  <div class="text-gray-900 bg-gray-100 leading-normal">
    <div class="p-4 max-w-5xl mx-auto">
      <img
        class="mx-auto my-8 max-w-full sm:max-w-sm"
        src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/45561/undraw_Ordinary_day_3gk3.svg"
        alt="A drawing of two houses in a neighborhood"
      />
      <h1 class="text-2xl md:text-4xl lg:text-5xl text-center my-4 font-black">
        <span class="concert-underline">Concert Breakfast Studio</span>
      </h1>
      <nav
        class="
          flex flex-col
          md:flex-row
          bg-gray-300
          rounded
          shadow
          overflow-hidden
          p-2
          mb-8
          text-sm
        "
      >
        <label class="sr-only" for="search">Search</label>
        <input
          @input="findMenu"
          v-model="query"
          class="mb-2 md:mb-0 p-2 rounded flex-grow"
          type="search"
          placeholder="Search for foods"
          id="search"
        />
        <select class="mb-2 md:ml-2 md:mb-0" @change="filterMenuGroups">
          <option value="">Food Groups</option>
          <option v-for="group in filterGroups" :key="group" :value="group">
            {{ group }}
          </option>
        </select>
        <button
          class="md:ml-2 p-2 rounded"
          style="background-color: var(--concert-blue)"
        >
          Place Order [0] (0)
        </button>
      </nav>
      <div class="grid mb-8">
        <!-- individual menu -->
        <breakfast-menu
          v-for="menu in dataKitchens"
          :key="menu.name"
          :name="menu.name"
          :image="menu.image"
          :groups="menu.groups"
          @addCart="cartHandler"
        />
        <!-- <nav
        class="flex flex-col md:flex-row bg-gray-300 rounded shadow overflow-hidden p-2 mb-8 text-sm"
      >
        <label class="sr-only" for="search">Search</label>
        <input
          class="mb-2 md:mb-0 p-2 rounded flex-grow"
          type="search"
          placeholder="Search for foods"
          id="search"
        >
        <select class="mb-2 md:ml-2 md:mb-0">
          <option>Food Groups</option>
        </select>
        <button
          class="md:ml-2 p-2 rounded"
          style="background-color: var(--concert-blue)"
        >Place Order [0] (0)</button>
      </nav> -->
      </div>
    </div>
  </div>
</template>

<script>
import BreakfastMenu from "./BreakfastMenu.vue";

export default {
  name: "BreakfastStudio",
  props: ["kitchens"],
  data() {
    return {
      query: "",
      dataKitchens: this.kitchens,
      initialDataMenu: this.kitchens,
      filterGroups: [],
      chart: []
    };
  },
  methods: {
    findMenu() {
      const result = this.kitchens.filter(
        (kitchen) =>
          kitchen.name.toLowerCase().indexOf(this.query.toLowerCase()) >= 0
      );
      this.dataKitchens = result;
    },
    filterMenuGroups(e) {
      if (e.target.length > 0) {
        const result = this.kitchens.filter((kitchen) =>
          kitchen.groups.includes(e.target.value.toLowerCase())
        );
        this.dataKitchens = result;
      }
    },
    cartHandler: function (data) {
      const menu = this.dataKitchens.find(({ name }) => name === data);

      this.chart.push(menu);
      // console.log(menu);
      return menu;
    },
  },
  mounted() {
    this.$nextTick(function () {
      const groups = [];
      this.dataKitchens.map((menu) => {
        menu.groups.map((value) =>
          groups.push(`${value.charAt(0).toUpperCase()}${value.slice(1)}`)
        );
      });

      const uniqueGroups = new Set(groups);
      const result = [...uniqueGroups];

      this.filterGroups = result;

      
    });

  },
  updated() {
console.log(this.chart);
  },
  components: {
    BreakfastMenu,
  },
};
</script>


<style>
:root {
  --concert-blue: #5fdce3;
}

.grid {
  display: grid;
  grid-gap: 1em;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.concert-underline {
  display: inline-block;
  position: relative;
  z-index: 0;
}

.concert-underline::after {
  display: inline-block;
  content: "";
  height: 1em;
  width: 100%;
  background: var(--concert-blue);
  left: 0;
  bottom: 0.25em;
  position: absolute;
  transform: skew(45deg) scale(0.9);
  z-index: -1;
  opacity: 0.5;
}

.concert-underline::before {
  display: inline-block;
  content: "";
  height: 1em;
  width: 100%;
  background: yellow;
  top: 0;
  left: -0.25em;
  position: absolute;
  transform: skew(45deg) scale(0.9) translateX(-0.5em);
  z-index: -1;
  opacity: 0.5;
}
</style>
