<template>
  <div id="app">
    <TreeCreator :myPackage="myPackage"/>
  </div>
</template>

<script>
import TreeCreator from "./components/TreeCreator.vue";
var packageChild = { packageName: "Child" };
var packageFather = {
  packageName: "Father",
  dep: [packageChild, packageChild, packageChild]
};
var packageGrandFather = {
  packageName: "GrandFather",
  dep: [packageChild, packageFather, packageChild, packageFather, packageChild]
};
export default {
  name: "app",
  data: function() {
    return {
      myPackage: {
        packageName: "FirstAncestor",
        dep: [
          packageFather,
          packageChild,
          packageGrandFather,
          packageChild,
          packageFather,
          packageGrandFather,
          packageFather,
          packageChild,
          packageChild
        ]
      }
    };
  },

  components: {
    TreeCreator
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
