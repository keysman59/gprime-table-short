<template>
    <div>
        <!-- <data-table-inset
            :columns="columns"
            @searchLayer="searchLayer"
        ></data-table-inset> -->
        <data-table-header
            :sorting="sorting"
        ></data-table-header>
        <button
            @click="showMore"
          >
            Подробнее
        </button>
        <button
            @click="delSelectItem"
          >
            Обнулить значение selectRow
        </button>
        <data-table-body
            :items="items"
            :columns="columns"
            :selectedRow="selectedRow"
            :selectedItems="selectedItems"
            @onCheckRow="onCheckRow"
            @selectedItems="selectedItems"
        ></data-table-body>
        <search-entity-description
            :selectedRow="selectedRow"
            ref="searchDescription"
        />
    </div>
</template>

<script>
import DataTableBody from './DataTableBody.vue'
// import DataTableInset from './DataTableInset'
import DataTableHeader from './DataTableHeader'
import SearchEntityDescription from './SearchEntityDescription.vue'

export default {
  components: { DataTableBody, SearchEntityDescription, DataTableHeader },
    name: 'DataTable',
    props: {
        items: Array,
        columns: Array,
        selectedRow: Object,
        selectedItems: Array,
    },
    data() {
        return {
            sorting: []
        }
    },
    watch: {
        columns () {
            this.setupColumns()
        }
    },
    created() {
        this.setupColumns()
    },
    methods: {
        onCheckRow (val) {
            this.$emit('onCheckRow', val)
        },
        delSelectItem () {
            this.selectedRow = {}
            console.log(this.selectedRow)
        },
        showMore () {
            this.$refs.searchDescription.openModal()
        },
        setupColumns () {
            console.log('setupColumns start')
            console.log('this.columns:')
            console.log(this.columns)
            this.sorting = this.columns.map(x => ({
                column: x,
                calculatedWidth: this.calculateColumnWidth(x)
            }))
            this.filters = this.columns.map(x => ({
                column: x,
                calculatedWidth: this.calculateColumnWidth(x),
                value: x.filter ? x.filter.value : null
            }))
        },
        searchLayer (layer) {
            this.selectedResult = null
            this.$emit('searchLayer', layer)
            this.$refs.searchDescription.closeModal()
            this.$emit('clearAllCheckbox')
        },
        calculateColumnWidth (column) {
            if (column.width) {
                return column.width
            }
            if (column.displayAs) {
                switch (column.displayAs) {
                case 'date':
                case 'input':
                    return this.getColumnWidthFromStringLength(column.title, 100, 150) + 'px'
                case 'datetime':
                    return this.getColumnWidthFromStringLength(column.title, 100, 170) + 'px'
                case 'number':
                    return this.getColumnWidthFromStringLength(column.title, 170, 180) + 'px'
                }
            }
            return this.getColumnWidthFromStringLength(column.title) + 'px'
        },
        getColumnWidthFromStringLength (str, minWidth = 150, maxWidth = 200) {
            const widthMultiplier = 10
            const widthAddingNumber = 20
            let width = str.length * widthMultiplier + widthAddingNumber

            if (width < minWidth) {
                width = minWidth
            }
            if (width > maxWidth) {
                width = maxWidth
            }
            return width
        },
    },
}
</script>