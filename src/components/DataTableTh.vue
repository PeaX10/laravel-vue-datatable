<template>
    <th
        scope="col"
        :key="column.name"
        :class="headerClasses(column)"
        class="laravel-vue-datatable-th"
        :style="'width: ' + column.width + '%'"
        @click="column.orderable  ? sort(column) : null">
        <div style="display: inline-block;" v-if="column.orderable">
            <div
                class="filter-asc"
                style="
                    width: 0;
                    height: 0;
                    margin-bottom: 1px;
                    border-bottom: 5px solid #ccc;
                    border-left: 5px solid transparent;
                    border-right: 5px solid transparent;"
                :class="{'active-filter-asc': column.orderable && column.name == currentSort && dir == 'asc' }"
                :style="{borderBottom: column.orderable && column.name == currentSort && dir == 'asc' ? '5px solid #a3a3a3' : '5px solid #ccc' }">
            </div>
            <div
                class="filter-desc"
                style="
                    width: 0;
                    height: 0;
                    margin-top: 1px;
                    border-top: 5px solid #ccc;
                    border-left: 5px solid transparent;
                    border-right: 5px solid transparent;"
                :class="{'active-filter-desc': column.orderable && column.name == currentSort && dir == 'desc' }"
                :style="{borderTop: column.orderable && column.name == currentSort && dir == 'desc' ? '5px solid #a3a3a3' : '5px solid #ccc' }">
            </div>
        </div>
        {{ column.label }}
    </th>
</template>

<script>
export default {
    data() {
        return {
            currentSort: '',
        };
    },
    props: {
        column: {
            type: Object,
            default: () => ({}),
            required: true,
        },
        classes: {
            type: Object,
            default: () => ({}),
        },
        dir: {
            type: String
        }
    },
    methods: {
        headerClasses(column) {
            let classes = this.classes;
            classes['table-header-sorting'] = column.orderable;
            return classes;
        },
        sort(column) {
            this.currentSort = column.name;
            this.$emit('sort', column);
        },
    }
}
</script>