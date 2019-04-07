<template>
  <div class="container">
    <h3>{{ myPackage.packageName}}</h3>
    <div v-if="Object.keys(dep).length">
      <button class="button" v-on:click="switchBtn">{{btnMsg}}</button>
    </div>
    <div v-if="showTree">
      <div v-if="Object.keys(dep).length">
        <div v-for="(Deppackage, key) in dep" :key="key">
          <TreeCreator :myPackage="Deppackage"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TreeCreator",
  props: ["myPackage"],
  data: function() {
    return { showTree: true, btnMsg: "-", dep: {} };
  },
  methods: {
    switchBtn() {
      this.showTree = !this.showTree;
      this.btnMsg = this.showTree ? "-" : "+";
    },
    thePromise() {
      return new Promise(resolve => {
        if (this.myPackage.dep) {
          setTimeout(() => {
            resolve(this.myPackage.dep);
          }, 1000);
        } else {
          resolve({});
        }
      });
    },
    thePromiseResult() {
      this.thePromise().then(data => {
        this.dep = data;
      });
    }
  },
  created() {
    this.thePromiseResult();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 0;
}
.container {
  display: flex;
  /* align-items: center; */
}
.button {
  margin: 5px;
  padding: 5px;
  border: 1px solid red;
  border-radius: 3px;
}
</style>
