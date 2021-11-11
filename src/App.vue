<template>
  <div id="app">
    <breakfast-studio
      :kitchens="kitchens"
      @customChange="logChange"
    />
    <!-- <BreakfastStudio
      v-for="kitchen in kitchens"
      :key="kitchen.name"
      :name="kitchen.name"
      :image="kitchen.image"
      :groups="kitchen.groups"
    ></BreakfastStudio> -->
    <!-- <BreakfastStudio /> -->
  </div>
</template>

<script>
import BreakfastStudio from "./components/BreakfastStudio";
import DUMMY_DATA from "./kitchen.js";

export default {
  name: "App",
  data: function () {
    return {
      kitchens: DUMMY_DATA,
    };
  },
  methods: {
   logChange(data) {
     console.log(data);
   }
  },
  mounted: function () {
    
  },
  components: {
    BreakfastStudio,
  },
};
</script>
    BreakfastStudio