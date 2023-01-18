<template>
  <div v-if="isShown" class="description">
    <div v-for="(attribute, index) of selectedRow.attributes" :key="index">
      {{ attribute.name }}
      {{ attribute.value }}
    </div>
  </div>
</template>

<script>

export default {

  props: {
    selectedRow: Object
  },
  data () {
    return {
      isShown: false,
      entityProperties: null,
      currentComponent: null
    }
  },
  methods: {
    closeModal () {
      this.isShown = false
    },
    openModal () {
      this.isShown = true
    },
  }
}
</script>

<style>

.description {
  height: 100px;

}

</style>