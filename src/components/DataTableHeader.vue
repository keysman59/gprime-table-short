<template>
    <div class="dt-header">
        <div v-for="(sort, index) of sorting" :key="index" class="dt-header-el">
            <div :key="index" @click="onSortField(sort)">
                <span>
                    <div class="text-container">
                    {{ sort.column.title }}
                    </div>
                </span>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'DataTableHeader',
    props: {
        sorting: Array
    },
    data() {
        return {
            selectedItem: false
        }
    },
    methods: {
        onSortField (sortField) {
            this.$emit('onSortField', sortField.column.field)
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
.dt-header {
    display: flex;
    padding-left: 24px;
}
.dt-header-el {
    width: 200px;
    text-align: center;
}


</style>