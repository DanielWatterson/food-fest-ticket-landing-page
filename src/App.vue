<template>
  <div :class="['app', theme]">
    <header class="site-header">
      <div class="nav-bar">
        <div class="logo">🎟️ TicketMaster</div>

        <h1 class="site-title">Event Tickets</h1>

        <!-- Wishlist counter -->
        <div class="wishlist">
          🎫 Your Tickets: <span>{{ wishlist.length }}</span>
        </div>

        <!-- Theme toggle -->
        <button class="theme-toggle" @click="toggleTheme">
          {{ theme === "dark" ? "Light Mode" : "Dark Mode" }}
        </button>

        <!-- Filters -->
        <div class="filters">
          <button
            @click="showAvailableOnly = false"
            :class="{ active: !showAvailableOnly }"
          >
            All Events
          </button>
          <button
            @click="showAvailableOnly = true"
            :class="{ active: showAvailableOnly }"
          >
            Available Only
          </button>
        </div>
      </div>
    </header>

    <main class="page-main">
      <div class="events-grid">
        <EventCard
          v-for="event in filteredEvents"
          :key="event.title"
          :event="event"
          :saved="!!wishlist.find((e) => e.title === event.title)"
          @add-to-wishlist="addToWishlist"
        />
      </div>
    </main>
  </div>
</template>

<script>
import EventCard from "./components/EventCard.vue";

export default {
  name: "App",
  components: { EventCard },

  data() {
    return {
      theme: "dark",
      showAvailableOnly: false,
      wishlist: [],
      events: [
        {
          title: "Fancy Feasts 2025",
          price: "R450",
          location: "Arena 7",
          date: "Dec 5, 2025",
          available: true,
          image: "https://i.postimg.cc/6QJSK0MQ/Fancy-Food-1.webp",
        },
        {
          title: "Cape Town Wine-Tasting Festival 2025",
          price: "R800",
          location: "Convention Center",
          date: "Nov 30, 2025",
          available: false,
          image: "https://i.postimg.cc/MG24wD9p/Wine-Festival.jpg",
        },
        {
          title: "Summer Music/Food Fest",
          price: "R600",
          location: "Beach Stage",
          date: "Dec 16, 2025",
          available: true,
          image: "https://i.postimg.cc/vmFjyz0B/Cape-Town-Street-Food.jpg",
        },
        {
          title: "Games, Glitz, Glamour & Grub 2026",
          price: "R300",
          location: "Expo Hall",
          date: "Mar 8, 2026",
          available: true,
          image:
            "https://i.postimg.cc/YSKV73d2/wooden-signs-pointing-to-food-games-music-festival-rustic-indicating-attractions-lively-promising-fu.webp",
        },
      ],
    };
  },

  computed: {
    filteredEvents() {
      return this.showAvailableOnly
        ? this.events.filter((e) => e.available)
        : this.events;
    },
  },

  methods: {
    toggleTheme() {
      this.theme = this.theme === "dark" ? "light" : "dark";
    },

    addToWishlist(event) {
      const index = this.wishlist.findIndex(
        (item) => item.title === event.title
      );
      if (index === -1) this.wishlist.push(event);
      else this.wishlist.splice(index, 1);
    },
  },

  watch: {
    theme(newVal) {
      if (typeof document !== "undefined") {
        document.body.classList.remove("dark", "light");
        document.body.classList.add(newVal);
      }
    },
  },

  mounted() {
    if (typeof document !== "undefined") {
      document.body.classList.add(this.theme);
    }
  },
};
</script>

<style>

/* Light/Dark page backgrounds are next to each other */
body.dark {
  background: linear-gradient(180deg, #000000, #1a1a1a);
  color: #e6e6e6;
}

body.light {
  background: linear-gradient(180deg, #f4f4f4, #e8e8e8);
  color: #111;
}

.app {
  min-height: 100vh;
}

.site-header {
  width: 100%;
  position: sticky;        
  top: 0;                   
  z-index: 50; 
}

.nav-bar {
  background: var(--header-bg);
  border-bottom: var(--header-border);
  box-shadow: var(--header-shadow);
  padding: 15px 25px;
  border-radius: 0 0 12px 12px;

  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 18px;
}

/* Theme-controlled colors */
.app.dark {
  --header-bg: rgba(20, 20, 20, 0.85);
  --header-border: 1px solid rgba(255, 255, 255, 0.12);
  --header-shadow: 0 4px 18px rgba(0, 0, 0, 0.65);
}

.app.light {
  --header-bg: rgba(255, 255, 255, 0.9);
  --header-border: 1px solid rgba(0, 0, 0, 0.08);
  --header-shadow: 0 4px 14px rgba(0, 0, 0, 0.18);
}

.logo {
  font-size: 1.8rem;
  font-weight: bold;
}

.site-title {
  margin: 0;
  font-size: 1.7rem;
  font-weight: 800;
  letter-spacing: 0.4px;
}

.wishlist {
  font-weight: bold;
  font-size: 1.2rem;
}

.theme-toggle {
  background: #ff00ff;
  border: none;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  color: white;
  font-weight: bold;
}

.filters {
  display: flex;
  gap: 10px;
}

.filters button {
  padding: 8px 12px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  background: #222;
  color: #fff;
  transition: 0.2s;
}

.filters button.active {
  background: #ff00ff;
  color: white;
}

.events-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
  padding: 20px 30px;
}

.app.dark .event-card {
  border: 1px solid rgba(255, 255, 255, 0.2);
  background: #111;
}

.app.light .event-card {
  border: 1px solid rgba(0, 0, 0, 0.2);
  background: #ffffffee;
}

.event-card:hover {
  transform: translateY(-6px) scale(1.02);
  box-shadow: 0 8px 26px rgba(0, 0, 0, 0.35);
  transition: 0.2s ease;
}

</style>
