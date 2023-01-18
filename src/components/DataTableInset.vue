<template>
    <div class="dt-inset">
        Datatable inset
        <div v-for="layer in columns" :key="layer.id" class="dt-inset__bookmark">
            <div :class="{ active: isActiveLayer === layer.id }" class="dt-inset__div" @click="searchLayer(layer)">
                {{ layer.name }}
                <div v-if="isActiveLayer === layer.id" class="dt-inset__decor-active-line"></div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'DataTableInset',
    props: {
        columns: Array
    },
    data() {
        return {

        }
    },
    methods: {
        searchLayer (layer) {
            this.isActiveLayer = layer.id
            this.$emit('searchLayer', layer)
        }
    }
}
</script>

<style scoped>

.dt-body-list {
    display: flex;
    flex-direction: column;
}
.dt-body-item {
    padding: 2px;
}


</style>