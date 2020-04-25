<template>
  <div class="field has-addons is-fullwidth">
    <div class="control is-expanded">
      <div class="dropdown is-active is-fullwidth">
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
      packagesSuggestions: []
    };
  },
  methods: {
    onFilterSuggestions: debounce(function() {
      searchPackages(this.filter).then(({ data }) => {
        this.packagesSuggestions = data;
      });
    }, 300),
    onClickSuggestion(packageValue) {
      getPackageInfo(
        packageValue.package.name,
        packageValue.package.version
      ).then(({ data }) => {
        console.log(data);
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
