<template>
    <div class="app">

    <HeaderBar :total="filtered.length" />

    <div class="bar-wrap">
        <SearchSortBar
            @update:search="val => search = val"
            @update:sort="val => sortOrder = val"
        />
    </div>

    <main class="grid">
        <PropertyCard
            v-for="p in pagedList"
            :key="p.id"
            :property="p"
            :bookmarked="bookmarks.includes(p.id)"
            @toggle-bookmark="toggleBookmark"
        />

        <div v-if="pagedList.length === 0" class="empty">
            No properties match your search.
        </div>
    </main>
    </div>
</template>

<script>
import properties from './data/properties'
import HeaderBar from './components/HeaderBar.vue'
import SearchSortBar from './components/SearchSortBar.vue'
import PropertyCard from './components/PropertyCard.vue'

export default {
    name: 'App',

    components: {
        HeaderBar,
        SearchSortBar,
        PropertyCard
    },

    data() {
        return {
        all: properties,
        search: '',
        sortOrder: 'default',
        bookmarks: JSON.parse(localStorage.getItem('pf_bookmarks') || '[]')
    }
    },

    computed: {
    filtered() {
        const q = this.search.trim().toLowerCase()

        let res = this.all.filter(p => {
            if (!q) return true
            return (
            p.title.toLowerCase().includes(q) ||
            p.location.toLowerCase().includes(q)
        )
        })

        if (this.sortOrder === 'low') {
            res = res.slice().sort((a, b) => a.price - b.price)
        } else if (this.sortOrder === 'high') {
            res = res.slice().sort((a, b) => b.price - a.price)
        }

        return res
    },

    pagedList() {
        return this.filtered
    }
    },

    methods: {
    toggleBookmark(id) {
        if (this.bookmarks.includes(id)) {
            this.bookmarks = this.bookmarks.filter(x => x !== id)
        } else {
            this.bookmarks.push(id)
        }
        localStorage.setItem('pf_bookmarks', JSON.stringify(this.bookmarks))
    }
    }
}
</script>

<style>

body {
    margin: 0;
    font-family: 'Inter', system-ui, sans-serif;
    background: linear-gradient(135deg, #eef2ff, #f7f9ff, #ffffff);
    background-attachment: fixed;
    color: #1b1c20;
}

.app {
    max-width: 1150px;
    margin: auto;
    padding: 28px;
}

.bar-wrap {
    margin: 20px 0 28px;
    background: rgba(255,255,255,0.45);
    backdrop-filter: blur(10px);
    padding: 16px 20px;
    border-radius: 18px;
    box-shadow: 0 6px 25px rgba(0,0,0,0.06);
}

.grid {
    display: grid;
    gap: 28px;
}

@media (min-width: 950px) {
    .grid {
        grid-template-columns: repeat(3, 1fr);
    }
}

@media (min-width: 650px) and (max-width: 949px) {
    .grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 649px) {
    .grid {
        grid-template-columns: 1fr;
    }
}

.empty {
    grid-column: 1 / -1;
    padding: 35px;
    text-align: center;
    background: rgba(255,255,255,0.6);
    border-radius: 18px;
    backdrop-filter: blur(8px);
    box-shadow: 0 4px 16px rgba(0,0,0,0.06);
    font-size: 1.15rem;
    font-weight: 600;
    color: #555;
}
</style>

