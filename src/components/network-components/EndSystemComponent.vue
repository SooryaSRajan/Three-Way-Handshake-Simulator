<template>
  <div :class="Class" :id="Id" class="rootElementEndSystem" :style="{top: top, left: left}">
    <div id="endSystemVector">
      <slot></slot>
    </div>
    <!--set package ID here so it can be used later -->
    <div v-if="isPackageSet && displayPackage" style="position: absolute; right: -88px" :id="packageId">
      <PackageComponent :data="data"></PackageComponent>
    </div>
  </div>
</template>

<script>

import PackageComponent from "@/components/network-components/PackageComponent";

export default {
  name: "EndSystemComponent",
  components: {PackageComponent},
  props: {
    Class: {
      type: String,
    },
    Id: {
      type: String,
    },
    packageId: {
      type: String,
    },
    top: {
      type: String,
    },
    left: {
      type: String,
    },
    data: {
      type: Array
    },
    displayPackage: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    packagePosition() {
      return "-50px"
    },
    isPackageSet() {
      return this.packageId !== undefined;
    }
  },
}
</script>

<style scoped>
.rootElementEndSystem {
  position: absolute;
}
div{
  transition: ease-in-out 1s;
}

</style>