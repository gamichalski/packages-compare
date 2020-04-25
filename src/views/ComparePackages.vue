<template>
  <div class="container is-fullheight is-fullcenter">
    <h1 class="title">Comparador de pacotes</h1>
    <search-packages-form />
    <div>Listagem</div>
  </div>
</template>

<script>
import SearchPackagesForm from "@/components/SearchPackagesForm";

export default {
  components: {
    SearchPackagesForm
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
