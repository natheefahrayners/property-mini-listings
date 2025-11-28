<template>
<header class="header">
<div class="brand">PropertyFinder</div>
<div class="meta">Total: <strong>{{total}}</strong></div>
</header>
</template>


<script>
export default {
name: 'HeaderBar',
props: {
total: { type: Number, required: true }
}
}
</script>


<style scoped>
.header {
display: flex;
justify-content: space-between;
align-items: center;
padding: 1rem 1.25rem;
}
.brand {
font-weight: 700;
font-size: 1.25rem;
}
.meta {
color: #333;
}
</style>