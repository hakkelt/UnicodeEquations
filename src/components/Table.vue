<template>
    <div id="table-container">
        <h3 id="table-desc">Available unicode characters:</h3>
        <div id="search">
            <input id="search-field" v-model="searchText" placeholder="search" />
            <div id="pages">
                <span>Current page: </span>
                <select v-model="current">
                    <option v-for="currentPage in pages" :key="currentPage" :value="currentPage">{{currentPage + 1}}</option>
                </select>
            </div>
        </div>
        
        <table aria-describedby="table-desc">
            <thead>
                <tr>
                    <th scope="col">Code point(s)</th>
                    <th scope="col">Character(s)</th>
                    <th scope="col">Replacement sequence(s)</th>
                    <th scope="col">Unicode name(s)</th>
                </tr>
            </thead>
            <tr v-for="record in pagedData" :key="record">
                <td>{{ record.code }}</td>
                <td>{{ record.char }}</td>
                <td>{{ typeof record.completion === 'string' ? record.completion : record.completion.join(', ') }}</td>
                <td>{{ record.name }}</td>
            </tr>
        </table>
    </div>
</template>

<style scoped>
#table-desc {
    margin-top: 2em;
}
#search {
    text-align: left;
    margin-bottom: 10px;
    height: 1em;
}
#search-field {
    float: left;
}
#pages {
    float: right;
}
#table-container {
    margin: auto;
    max-width: 800px;
    padding: 1em;
}
table {
    border-collapse: collapse;
}
table td, table th {
    border-style: solid;
    border-width: 1px;
    padding: 5px;
}
table th {
    background-color: lightyellow;
}
</style>

<script>
import data from './codeTable';
const pageSize = 30;
export default {
    data() {
        return {
            records: data,
            searchText: '',
            current: 0
        };
    },
    computed: {
        filteredData() {
            if (this.searchText == '')
                return this.records;
            else {
                const srcTxt = this.searchText.toLowerCase();
                return this.records
                    .filter(record =>
                        (typeof record.name === 'string') && record.name.toLowerCase().search(srcTxt) != -1
                        || (typeof record.completion === 'string') && record.completion.toLowerCase().search(srcTxt) != -1);
            }
        },
        pagedData() {
            return this.filteredData.slice(this.current * pageSize, (this.current + 1) * pageSize);
        },
        pages() {
            return [...Array(Math.ceil(this.filteredData.length / pageSize)).keys()];
        }
    }
}
</script>
