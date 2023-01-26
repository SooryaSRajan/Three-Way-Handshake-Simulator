<template>
  <div class="flex-box">
    <TopBar title="Simulation of the TCP Protocol"></TopBar>
    <div class="rem-space">
      <div class="row-1">
        hey
      </div>
      <div class="row-2">
        <NetworkInteractionComponent ref="childComponentRef">
          <EndSystemComponent class="box" id="computer1" package-id="package1" top="55%" left="10%"
                              :data="packageData" :display-package="displayPackage">
            <img src="./assets/desktop.png" width="150" height="150" alt="computer">
          </EndSystemComponent>
          <EndSystemComponent class="box" id="computer2" top="10%" left="70%">
            <img src="./assets/desktop.png" width="150" height="150" alt="computer">
          </EndSystemComponent>
        </NetworkInteractionComponent>
        <button @click="begin(1234)">Start animation</button>
        <button @click="stepTwo(5678)">Step 2</button>
        <button @click="stepThree()">Step 3</button>
      </div>
    </div>
  </div>
</template>

<script>

import TopBar from "@/components/TopBar";
import NetworkInteractionComponent from "@/components/network-components/NetworkInteractionComponent";
import EndSystemComponent from "@/components/network-components/EndSystemComponent";

export default {
  name: 'App',
  components: {EndSystemComponent, NetworkInteractionComponent, TopBar},
  mounted() {
    this.$refs.childComponentRef.drawLine("computer1", "computer2")
  },
  data() {
    return {
      packageData: [],
      displayPackage: false
    }
  },
  methods: {
    begin(number) {
      if (number.toString().length === 4 && !isNaN(number)) {
        // this.packageData = []
        this.packageData.push(number)
        this.displayPackage = true
        setTimeout(() => {
          this.$refs.childComponentRef.animatePackageNew("computer2", "package1", "computer1")
        }, 1000)

      } else {
        this.displayPackage = false
      }
    },
    stepTwo(number) {
      if (number.toString().length === 4 && !isNaN(number)) {
        this.packageData[this.packageData.length - 1] = this.packageData[this.packageData.length - 1] + 1
        this.packageData.push(number)
        this.displayPackage = true
        setTimeout(() => {
          this.$refs.childComponentRef.animatePackageNew("computer1", "package1", "computer2")
        }, 1000)

      } else {
        this.displayPackage = false
      }
    },
    stepThree() {
      this.packageData[this.packageData.length - 1] = this.packageData[this.packageData.length - 1] + 1
      this.displayPackage = true
      setTimeout(() => {
        this.$refs.childComponentRef.animatePackageNew("computer2", "package1", "computer1")
      }, 1000)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.flex-box {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100%;
}

.rem-space {
  flex: 1;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.row-1 {
  flex: 2;
  min-width: 300px;
}

.row-2 {
  flex: 5;
  width: 100%;
  height: 100%;
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {
  height: 100vh;
  width: 100vw;
}

</style>
