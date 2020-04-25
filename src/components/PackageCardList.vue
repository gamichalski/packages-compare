<template>
  <div class="columns is-multiline is-fullwidth">
    <div
      class="column is-4"
      v-for="(packageValue, index) in packages"
      :key="index"
    >
      <div class="card">
        <div class="card-content">
          <a
            class="button is-danger is-outlined is-small is-pulled-right"
            @click="$emit('remove', packageValue, index)"
            >Remover</a
          >
          <a
            class="button is-small is-pulled-right"
            :href="`https://www.npmjs.com/package/${packageValue.name}`"
            target="_blank"
            >Acessar</a
          >
          <p class="title is-4">
            {{ packageValue.name }}@{{ packageValue.version }}
          </p>
          <p>Tamanho {{ packageValue.gzip / 10000 }} MB</p>
          <p>{{ packageValue.dependencyCount }} Dependencias</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    packages: Array
  }
};
</script>

<style lang="scss" scoped>
.is-fullwidth {
  width: 100%;
}
</style>
