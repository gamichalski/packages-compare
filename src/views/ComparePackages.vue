<template>
  <div class="container is-fullheight is-fullcenter">
    <h1 class="title">Comparador de pacotes</h1>
    <search-packages-form @found="onFoundPackage" />
    <package-card-list :packages="packages" @remove="onClickRemove" />
  </div>
</template>

<script>
import SearchPackagesForm from "@/components/SearchPackagesForm";
import PackageCardList from "@/components/PackageCardList";

export default {
  components: {
    SearchPackagesForm,
    PackageCardList
  },
  data() {
    return {
      packages: []
    };
  },
  methods: {
    onFoundPackage(packageInfo) {
      this.packages.push(packageInfo);
    },
    onClickRemove(packageInfo, index) {
      this.packages.splice(index, 1);
    }
  }
};
</script>

<style lang="scss" scoped>
.is-fullheight {
  height: 100vh;
}
.is-fullcenter {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
