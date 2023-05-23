<template>
  <h1>API Demo</h1>
  {{ title }}
  <!-- <button @click="makeTitleLower()">Set Title toLowerCase()</button> -->
  {{ makeTitleLowerCompute }}
  {{ title }}
</template>

<script>
export default {
  name: "ApiDemo",
  components: {},
  props: {},
  data() {
    return {
      title: "Life CYCLE Hooks",
    };
  },
  methods: {
    /*makeTitleLower() {
      return this.makeTitleLowerCompute;
    },*/
  },
  computed: {
    makeTitleLowerCompute() {
      console.log("computed....");
      return this.title.toLowerCase();
    },
  },
  beforeCreate() {
    console.log("beforeCreate() from child...");
  },
  created() {
    console.log("created() from child...");
  },
  beforeMount() {
    console.log("beforeMount() from child...");
  },
  mounted() {
    console.log("mounted() from child...");
  },
  beforeUpdate() {
    console.log("beforeUpdate() from child...");
  },
  updated() {
    console.log("updated() from child...");
  },
  beforeUnmount() {
    console.log("beforeUnmount() from child...");
  },
  unmounted() {
    console.log("unmounted() from child...");
  },
};
</script>
