<script>
import CardBoard from "./components/CardBoard.vue";
import CardForm from "./components/CardForm.vue";
import FilterBar from "./components/FilterBar.vue";

export default {
  name: "App",
  components: {
    CardBoard,
    CardForm,
    FilterBar,
  },
  data() {
    return {
      myName: "My name",
      showList: [
        {
          id: 1,
          title: "Breaking Bad",
          description:
            "A high school chemistry teacher turned methamphetamine producer",
          image: "https://www.coverwhiz.com/uploads/tv/breaking-bad-season-1.jpg",
          rating: 5,
          tags: ["drama", "crime", "thriller"],
          notes:
            "An impressive series about the transformation of an ordinary man into a criminal.",
          color: "#2e6136",
          releaseDate: "2008-01-20",
        },
        {
          id: 2,
          title: "Stranger Things",
          description:
            "A group of kids uncovering supernatural mysteries in their town",
          image:
            "https://www.coverwhiz.com/uploads/tv/stranger-things-season-1_small.jpg",
          rating: 4.5,
          tags: ["sci-fi", "horror", "mystery"],
          notes: "A perfect blend of 80s nostalgia and science fiction.",
          color: "#612e36",
          releaseDate: "2016-07-15",
        },
        {
          id: 3,
          title: "The Walking Dead",
          description: "Survivors of a zombie apocalypse fight to stay alive",
          image: "https://www.coverwhiz.com/uploads/tv/the-walking-dead-season-1.jpg",
          rating: 3,
          tags: ["horror", "drama", "action"],
          notes: "An intense series about survival in a post-apocalyptic world.",
          color: "#2e3461",
          releaseDate: "2010-10-31",
        },
        {
          id: 4,
          title: "Game of Thrones",
          description: "Noble families vie for control of the Iron Throne",
          image: "https://www.coverwhiz.com/uploads/tv/game-of-thrones-season-1.jpg",
          rating: 4,
          tags: ["fantasy", "drama", "action"],
          notes: "An epic tale of power, betrayal, and war.",
          color: "#61362e",
          releaseDate: "2011-04-17",
        },
        {
          id: 5,
          title: "American Horror Story",
          description: "An anthology series centering on different characters and locations, including a haunted house, an insane asylum, a witch coven, a freak show, a hotel, a possessed farmhouse, a cult, the apocalypse, and a summer camp.",
          image: "https://www.coverwhiz.com/uploads/tv/american-horror-story-season-1-murder-house.jpg",
          rating: 4.2,
          tags: ["horror", "drama", "thriller"],
          notes: "A chilling anthology series with a new story each season.",
          color: "#000000",
          releaseDate: "2011-10-05",
        },
      ],
    };
  },
};
</script>

<template>
  <header class="main-header">
    <div class="logo">
      <img src="/src/assets/logo.png" alt="logo" />
    </div>
    <h1>TV Show Manager: {{ myName }}</h1>
  </header>
  <main class="main">
    <FilterBar />
    <div class="shows-container">
      <CardBoard class="shows-container__board" :show-list="showList" />
      <CardForm class="shows-container__form" v-if="true" />
    </div>
  </main>
</template>

<style scoped>
/* Header */
.main-header {
  height: 75px;
  display: grid;
  grid-template-columns: 70px 1fr;
  align-items: center;
  gap: 10px;
}

.logo img {
  height: 100%;
  width: 100%;
  object-fit: contain;
}

/* Wrapper below header */
.main {
  min-height: calc(100vh - 100px);
}

/* Container for CardBoard and CardForm */
.shows-container {
  display: flex;
  flex-direction: row;
  gap: 20px;
}

.shows-container__board {
  flex: 70% 1 0;
}
</style>
