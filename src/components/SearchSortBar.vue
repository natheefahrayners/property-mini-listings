<template>
<div class="searchbar">
<input
v-model="q"
@input="$emit('update:search', q)"
placeholder="Search by title or location..."
aria-label="search"
/>


<select v-model="sort" @change="$emit('update:sort', sort)">
<option value="default">Sort: Default</option>
<option value="low">Price: Low → High</option>
<option value="high">Price: High → Low</option>
</select>
</div>
</template>


<script>
export default {
name: 'SearchSortBar',
props: {
modelValue: String
},
data() {
return {
q: '',
sort: 'default'
}
}
}
</script>


<style scoped>
.searchbar {
display: flex;
gap: 0.5rem;
padding: 0.75rem 1rem;
align-items: center;
}
.searchbar input {
flex: 1;
padding: 0.5rem 0.75rem;
border-radius: 8px;
border: 1px solid #ddd;
}
.searchbar select {
padding: 0.5rem;
border-radius: 8px;
border: 1px solid #ddd;
}
</style>