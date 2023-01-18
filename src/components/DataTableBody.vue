<template>
    <div class="dt-body-list">
        <div v-for="(item, index) in items" :key="index" class="dt-body-item">
            <div class="dt-body-row">
                <input type="checkbox" @click="onCheckRow(item)">
                <div
                    class="dt-body-inner"
                    v-for="(column, columnIndex) of columns"
                    :key="columnIndex">
                        {{ getValue(item.attributes, column) }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'DataTableBody',
    props: {
        items: Array,
        columns: Array,
        selectedRow: Object,
        selectedItems: Array,
    },
    data() {
        return {

        }
    },
    methods: {
        onCheckRow(row) {
            console.log('row', row)
            console.log('this.selectedItems', this.selectedItems)
            this.$emit('onCheckRow', row)
        },
        getValue (item, column) {

            let columnValue
            item.forEach(el => {
                if (el.name === column.field) {
                columnValue = el.value
                }
            })
            return columnValue
        },
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
    margin-top: 5px;
    margin-bottom: 5px;
}
.dt-body-row {
    display: flex;
    text-align: center;
}
.dt-body-inner {
    max-width: 200px;
    width: 100%;
}


</style>