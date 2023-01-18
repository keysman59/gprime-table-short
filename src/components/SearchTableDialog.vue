<template>
    <div>
        SearchTableDialog
        <data-table
            :items="items"
            :columns="columns"
            :inset="inset"
            :selectedRow="selectedRow"
            :selectedItems="selectedItems"
            @onCheckRow="onCheckRow"
        ></data-table>
    </div>
</template>

<script>
import DataTable from './DataTable'
import { localItems } from '../data/items.js'
import { localResults } from '../data/results.js'
import { localColumns } from '../data/columns.js'
import { localInset } from '../data/inset.js'


export default {
    name: 'SearchTableDialog',
    data() {
        return {
            lastSortField: '',
            items: [],
            columns: [],
            inset: [],
            selectedRow: {},
            selectedItems: []
        }
    },
    methods: {
        onCheckRow (row) {
            this.selectedRow = row
            this.selectedItems.push(row)
        }
    },
    components: {
        DataTable
    },
    created() {
        this.items = localItems
        this.results = localResults
        this.columns = localColumns
        this.inset = localInset
    }
}
</script>