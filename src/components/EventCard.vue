<template>
  <div class="event-card" :aria-pressed="saved ? 'true' : 'false'">
    <div class="image-container">
      <img :src="event.image" :alt="event.title" />
      <div v-if="!event.available" class="sold-overlay">SOLD OUT</div>
    </div>

    <h2 class="card-title">{{ event.title }}</h2>
    <p class="details">{{ event.date }} • {{ event.location }}</p>
    <p class="price">{{ event.price }}</p>

    <div class="button-row">
      <button
        class="book-btn"
        :disabled="!event.available"
        @click="bookEvent(event.title)"
      >
        {{ event.available ? "Book Now" : "Unavailable" }}
      </button>

      <button
        class="save-btn"
        :class="{ saved: saved }"
        @click="toggleSave"
        aria-pressed="saved ? true : false"
      >
        {{ saved ? "Remove" : "Save" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "EventCard",
  props: {
    event: { type: Object, required: true },
    saved: { type: Boolean, default: false },
  },
  methods: {
    bookEvent(title) {

      alert(`You booked: ${title}`);
    },
    toggleSave() {
      this.$emit("add-to-wishlist", this.event);
    },
  },
};
</script>

<style scoped>
.event-card {
  padding: 18px;
  border-radius: 14px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  gap: 12px;
  transition: all 0.2s;
  text-align: center;
}


.image-container {
  width: 100%;
  height: 160px;                     
  position: relative;
  overflow: hidden;
  border-radius: 8px;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}


.sold-overlay {
  position: absolute;
  inset: 0;
  background: rgba(255, 0, 255, 0.45);
  color: white;
  font-weight: bold;
  font-size: 22px;
  display: flex;
  justify-content: center;
  align-items: center;
}


h2 {
  margin: 8px 0 2px;
  font-size: 1.1rem;
}

.details {
  font-size: 0.9rem;
  color: var(--details-color);
  margin-bottom: 4px;
}

.price {
  font-weight: bold;
  font-size: 1rem;
  margin-bottom: 10px;
}


.button-row {
  display: flex;
  gap: 10px;
  margin-top: auto;
}


.button-row button {
  flex: 1;
  padding: 9px 12px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}

.button-row button.saved {
  background: #ff00ff;
  color: white;
}

.button-row button:not(.saved) {
  background: #00e0e0;
  color: #111;
}

.button-row button:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

</style>
