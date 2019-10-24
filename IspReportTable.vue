<template>
    <div :class="data.class.main">
        <div :class="data.class.legend_container">
            <component
                    v-bind:root_data="data_legend"
                    v-bind:is="column_legend">
            </component>
        </div>
        <div :class="data.class.data_container">
            <div :class="data.class.data_column" v-bind:item="item" v-for="item in data_view" v-if="data_view.length">
                <component
                        v-bind:root_data="item"
                        v-bind:is="column_data">
                </component>
            </div>
            <div :class="data.class.data_column" v-if="!data_view.length || show_empty">
                <div :class="data.class.empty_row" v-on:click="column_empty">
                    Нет данных для отображения
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            data_view: {
                type: Array,
                required: true
            },
            data_legend: {
                type: Object,
                default: () => {
                    return {}
                },
                required: false
            },
            column_legend: {
                type: Object,
                required: true,
            },
            column_data: {
                type: Object,
                required: true,
            },
            column_empty: {
                type: Function,
                default: function () {
                    console.log('click on empty row');
                },
                required: false
            },
            show_empty: {
                type: Boolean,
                default: false,
                required: false
            },
        },
        data: function () {
            return {
                data: {
                    class: {
                        'main': 'DataTable',
                        'legend_container': 'DataTable_Legend_Container',
                        'legend_row': 'DataTable_Legend_Container_Row',
                        'data_container': 'DataTable_Data_Container',
                        'data_column': 'DataTable_Data_Column',
                        'empty_row': 'DataTable_Data_Column_Empty',
                    },
                },
            }
        },
    }
</script>

<style>
    .DataTable {
        width: 100%;
        display: flex;
    }

    .DataTable_Legend_Container {
        max-width: 200px;
        width: 100%;
    }

    .DataTable_Legend_Container_Row {
        width: 100%;
        text-align: center;
        border-left: 1px dotted gray;
        border-right: 1px dotted gray;
        background-color: rgba(128, 128, 128, 0.2);
        font-size: 1rem;
    }

    .DataTable_Data_Container {
        width: calc(100% - 210px);
        overflow-x: auto;
        display: flex;
        padding-bottom: 1rem;
    }

    .DataTable_Data_Column {
        max-width: 320px;
        min-width: 275px;
        margin-left: 0.5rem;
        margin-right: 0.5rem;
    }

    .DataTable_Data_Column_Row {
        display: block;
        border-left: 1px dotted gray;
        border-right: 1px dotted gray;
        border-bottom: 1px dotted gray;
        font-size: 1rem;
    }

    .DataTable_Data_Column_Row_Name {
        display: none;
        border-left: 1px dotted gray;
        border-right: 1px dotted gray;
        border-bottom: 1px dotted gray;
        font-size: 1rem;
        text-align: center;
        font-weight: bold;
    }

    .DataTable_Data_Column_Row .col-12 {
        min-height: 20px;
    }

    .DataTable_Data_Column_Empty {
        /*padding: 5px;*/
        color: rgba(128, 128, 128, 0.8);
        text-align: center;
        /*font-size: 2rem;*/
    }

    .DataTable_Data_Column_Empty:hover {
        cursor: pointer;
        background-color: #dbdbdb;
    }

    .DataTable_Data_Column:hover {
        background-color: #dbdbdb !important;
    }

    @media (max-width: 768px) {
        .DataTable_Legend_Container {
            display: none;
        }

        .DataTable_Data_Container {
            width: 100%;
            flex-wrap: wrap;
            overflow: visible;
            justify-content: center;
        }

        .DataTable_Data_Column {
            width: 310px;
            border: 1px solid black;
            margin-top: 2rem;
        }

        .DataTable_Data_Column_Row {
            margin-top: 0 !important;
        }

        .DataTable_Data_Column_Row_Name {
            display: block;
        }
    }


</style>