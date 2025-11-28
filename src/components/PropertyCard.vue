<template>
    <article class="card">
        <div class="img-wrap">
        <img :src="property.image" :alt="property.title" />

        <span v-if="!property.available" class="badge">
            Not Available
        </span>

        <button 
            class="bookmark-btn" 
            @click="$emit('toggle-bookmark', property.id)"
            :title="bookmarked ? 'Remove Bookmark' : 'Save Property'"
        >
            <span v-if="bookmarked">★</span>
            <span v-else>☆</span>
        </button>
        </div>

    <div class="card-body">
        <h3 class="title">{{ property.title }}</h3>

        <p class="meta">
            {{ property.type }} • {{ property.location }}
        </p>

        <div class="info-row">
            <div class="price">R {{ formatPrice(property.price) }}</div>
        </div>
        </div>
    </article>
</template>

<script>
export default {
    name: "PropertyCard",
    props: {
        property: { type: Object, required: true },
        bookmarked: { type: Boolean, default: false }
    },
    methods: {
    formatPrice(n) {
        return n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
    } 
};
</script>

<style scoped>

.card {
    background: rgba(255, 255, 255, 0.75);
    backdrop-filter: blur(14px);
    border-radius: 20px;
    box-shadow: 0 12px 32px rgba(15, 15, 20, 0.08);
    overflow: hidden;
    transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.card:hover {
    transform: translateY(-6px);
    box-shadow: 0 16px 40px rgba(15, 15, 20, 0.12);
}

.img-wrap {
    position: relative;
}

.img-wrap img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    display: block;
}

.bookmark-btn {
    position: absolute;
    right: 0.8rem;
    top: 0.8rem;
    background: rgba(255,255,255,0.85);
    border: none;
    font-size: 1.4rem;
    padding: 6px 10px;
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.25s;
}

.bookmark-btn:hover {
    background: #ffffff;
}

.badge {
    position: absolute;
    left: 0.8rem;
    top: 0.8rem;
    padding: 0.35rem 0.7rem;
    font-size: 0.75rem;
    font-weight: 600;
    border-radius: 12px;
    color: #fff;
    background: linear-gradient(135deg, #ff416c, #ff4b2b);
    box-shadow: 0 4px 12px rgba(255, 65, 108, 0.35);
}

.card-body {
    padding: 1.1rem 1.2rem 1.4rem;
}

.title {
    font-size: 1.1rem;
    font-weight: 700;
    color: #1b1c20;
    margin-bottom: 0.4rem;
}

.meta {
    font-size: 0.87rem;
    color: #6c6f75;
    margin-bottom: 0.9rem;
}

.price {
    font-size: 1.2rem;
    font-weight: 700;
    color: #3b1dff;
}

.info-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>
