<template>
  <div class="field has-addons is-fullwidth">
    <div
      class="control is-expanded is-large"
      :class="{ 'is-loading': isLoading }"
    >
      <div
        class="dropdown is-fullwidth"
        :class="{ 'is-active': !isEmptySuggestions }"
      >
        <input
          class="input is-large is-fullwidth"
          v-model="filter"
          @keyup="onFilterSuggestions"
        />
        <div class="dropdown-menu is-fullwidth" id="dropdown-menu" role="menu">
          <div class="dropdown-content">
            <a
              v-for="(packageValue, index) in packagesSuggestions"
              :key="index"
              @click="onClickSuggestion(packageValue)"
              class="dropdown-item"
            >
              {{ packageValue.package.name }}@{{ packageValue.package.version }}
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="control">
      <a class="button is-large" @click="onFilterSuggestions">
        Buscar
      </a>
    </div>
  </div>
</template>

<script>
import { searchPackages, getPackageInfo } from "@/services/packages";
import debounce from "lodash/debounce";

export default {
  data() {
    return {
      filter: "",
      isLoading: false,
      packagesSuggestions: []
    };
  },
  computed: {
    isEmptySuggestions() {
      return this.packagesSuggestions.length === 0;
    }
  },
  methods: {
    onFilterSuggestions: debounce(function() {
      this.isLoading = true;
      if (this.filter) {
        searchPackages(this.filter)
          .then(({ data }) => {
            this.packagesSuggestions = data;
          })
          .finally(() => {
            this.isLoading = false;
          });
      } else {
        this.packagesSuggestions = [];
        this.isLoading = false;
      }
    }, 300),
    onClickSuggestion(packageValue) {
      getPackageInfo(
        packageValue.package.name,
        packageValue.package.version
      ).then(({ data }) => {
        this.$emit("found", data);
        this.filter = "";
        this.packagesSuggestions = [];
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.is-fullwidth {
  width: 100%;
}
</style>
