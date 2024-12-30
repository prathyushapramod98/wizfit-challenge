<template>
  <div>
    <!-- Header Section -->
    <header class="header"/>
    <div class="header-overlay">
      <div class="header-content">
        <h1 class="header-title">What is WizFit Challenge?</h1>
        <button class="watch-video-btn">Watch Video</button>
      </div>
    </div>
    <!-- Main Content -->
    <main class="main-content">
      <!-- Challenge Info Section -->
      <img src="./assets/player.png" alt="Harlem Wizard Player" class="player-image" />

      <section class="challenge-info">
        <h2>Are you ready to take the challenge?</h2>
        <p>Download Harlem Wizards App</p>
        <div class="app-links">
          <a href="https://play.google.com/store"><img src="./assets/google-store.png" alt="Google Store" /></a>
          <a href="https://www.apple.com/app-store/"><img src="./assets/apple-store.png" alt="Apple Store" /></a>
        </div>

        <!-- Search bar -->
        <SearchBar @onSearch="fetchSchools" />

        <div v-if="isLoading" class="loading">Loading...</div>
        
        <div v-else class="school-items">
          <div v-if="schools.length === 0" class="no-results">No schools found. Try a different search.</div>
          <div v-else v-for="school in schools" :key="school.id" class="school-item">
            <span>{{ school.campaign_detail.sub_domain }}</span>
            <button class="join-btn">Join Campaign</button>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import SearchBar from "@/components/SearchBar.vue";
import axios from "axios";

export default {
  components: { SearchBar },
  data() {
    return {
      schools: [],
      isLoading: false,
    };
  },
  methods: {
    async fetchSchools(query = "") {
      this.isLoading = true;
      try {

        const url = query
          ? `http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${query}`
          : 'https://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=';
        const response = await axios.get(url);
        this.schools = response.data.school_list
          || [];
        console.log(this.schools, 'sssss')
      } catch (error) {
        console.error("Error fetching schools:", error);
      } finally {
        this.isLoading = false;
      }
    }

  },
  created() {
    this.fetchSchools();
  },
};
</script>
<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
}

/* Header */
.header {
  background: url("./assets/header.png");
  height: 300px;
  width: 100vw;
  margin: 0;
}

.header-overlay {
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  text-align: center;
  padding: 20px;
}

.header-content {
  display: flex;
  align-items: center;
  gap: 20px;
}

.header-title {
  font-size: 2.5rem;
  margin: 0;
  color: #f54b64;
  font-weight: bold;
}

.watch-video-btn {
  padding: 10px 20px;
  background-color: #f54b64;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

/* Main Content */
.main-content {
  padding: 20px;
  text-align: center;
  margin-top: 20px;
}

/* Challenge Info Section */
.challenge-info {
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  margin: 20px auto;
  width: 80%;
  max-width: 600px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.player-image {
  width: 180px;
  margin: 15px 0;
}

.challenge-info h2 {
  color: #f54b64;
  font-weight: bold;
}

.app-links {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.app-links img {
  width: 140px;
  transition: transform 0.3s;
}

.app-links img:hover {
  transform: scale(1.1);
}

/* School List Section */

.school-items {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.school-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 80%;
  max-width: 600px;
  margin: 10px 0;
  padding: 10px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.no-results,
.loading {
  font-size: 1.2rem;
  color: #555;
}

.join-btn {
  background-color: #f54b64;
  color: white;
  border: none;
  padding: 5px 15px;
  border-radius: 5px;
  cursor: pointer;
}

@media (max-width: 1024px) {

  /* Header */
  .header-title {
    font-size: 2.2rem;
  }

  .header-content {
    flex-direction: column;
    gap: 10px;
  }

  .watch-video-btn {
    font-size: 1rem;
    padding: 8px 16px;
  }

  /* Challenge Info Section */
  .challenge-info {
    width: 90%;
    padding: 15px;
  }

  .player-image {
    width: 160px;
  }

  /* App Links */
  .app-links {
    gap: 15px;
  }

  .app-links img {
    width: 130px;
  }

  /* School List */
  .school-item {
    width: 90%;
    flex-direction: column;
    align-items: flex-start;
    padding: 15px;
  }

  .join-btn {
    margin-top: 10px;
  }
}

@media (max-width: 768px) {

  /* Header */
  .header-title {
    font-size: 2rem;
  }

  .header-content {
    flex-direction: column;
    gap: 10px;
  }

  /* Challenge Info Section */
  .challenge-info {
    width: 95%;
    padding: 10px;
  }

  .player-image {
    width: 140px;
  }

  /* App Links */
  .app-links {
    flex-direction: column;
    gap: 10px;
  }

  .app-links img {
    width: 120px;
  }

  /* School List */
  .school-item {
    width: 100%;
    flex-direction: column;
    align-items: flex-start;
    padding: 12px;
  }

  .join-btn {
    margin-top: 10px;
  }

  .no-results,
  .loading {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {

  /* Header */
  .header-title {
    font-size: 1.8rem;
  }

  .header-content {
    gap: 5px;
  }

  .watch-video-btn {
    padding: 8px 16px;
    font-size: 0.9rem;
  }

  /* Challenge Info Section */
  .challenge-info {
    width: 100%;
    padding: 8px;
  }

  .player-image {
    width: 120px;
  }

  /* App Links */
  .app-links {
    gap: 10px;
  }

  .app-links img {
    width: 100px;
  }

  /* School List */
  .school-item {
    width: 100%;
    flex-direction: column;
    align-items: flex-start;
    padding: 10px;
  }

  .join-btn {
    margin-top: 10px;
  }

  .no-results,
  .loading {
    font-size: 0.9rem;
  }
}
</style>
