<template>
    <div :class="['museum-highlight', isPartner ? 'museum-highlight--partner' : 'museum-highlight--museum']">
      <!-- Badge for Space Page -->
      <div class="museum-highlight__badge">
        <img v-if="isPartner" src="../assets/star.svg" alt="Star badge" />
        <!-- Add badges for other pages (Dinosaur, Oceans, etc.) here -->
      </div>
  
      <img :src="highlight.image" alt="Highlight image" class="museum-highlight__image" />
  
      <div class="museum-highlight__details">
        <h3 class="museum-highlight__title">{{ highlight.name }}</h3>
        <p class="museum-highlight__description">{{ highlight.description || highlight.info }}</p>
        <p class="museum-highlight__date">{{ new Date(highlight.date).toLocaleDateString() }}</p>
  
        <!-- Optional News section -->
        <div v-if="highlight.news" class="museum-highlight__news">
          <strong>News:</strong> {{ highlight.news.title }}
        </div>
  
        <div class="buttons">
            <a v-if="highlight.quiz" :href="highlight.quiz" target="_blank" class="museum-highlight__quiz-link">
              Take the quiz
            </a>
      
            <!-- Refresh image button -->
            <button @click="$emit('refresh-image', highlight.id)" class="museum-highlight__refresh-btn">
              Refresh image
            </button>
        </div>
        <!-- Optional Quiz link for Space page -->
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MuseumHighlight',
    props: {
      highlight: {
        type: Object,
        required: true,
      },
      isPartner: {
        type: Boolean,
        default: false,
      },
    },
  };
  </script>
  
  <style lang="scss" scoped>
  .museum-highlight {
    display: flex;
    flex-direction: column;
    width: 20%;
    padding: 16px;
    border-radius: 8px;
    background-color: #fff;
    position: relative;
  
    &__badge {
      position: absolute;
      top: 2px;
      right: 2px;
    }
  
    &__image {
      width: 100%;
      height: 120px;
      object-fit: cover;
      margin-bottom: 16px;
    }
  
    &__details {
      height: 244px;
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      font-size: 14px;
    }
  
    &__title {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 8px;
    }
  
    &__description {
      font-size: 14px;
      color: #666;
      margin-bottom: 16px;
    }
  
    &__news {
      font-size: 12px;
      margin-bottom: 16px;
      color: #333;
    }
  
    &__quiz-link {
      font-size: 12px;
      color: #007bff;
      text-decoration: none;
    }

    .buttons {
        display: flex;
        justify-content: space-evenly;
        align-items: baseline;
    }
  
    &__refresh-btn {
      background-color: #536273;
      color: white;
      border: none;
      padding: 8px;
      cursor: pointer;
      border-radius: 4px;
      margin-top: 16px;
    }

    &__description, &__title, &__news, &__date {
        text-align: left;
    }
  }
  </style>
  