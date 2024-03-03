<!-- BhagavadGitaSummary.vue -->

<template>
  <div>
    <h1>Bhagvad Gita Chapters Summary</h1>
    <div class="container">
      <div v-for="chapter in chapters" :key="chapter.chapter_number" class="card">
        <p class="c_no">Chapter {{ chapter.chapter_number }}</p>
        <p class="c_name">{{ chapter.name_transliterated }}</p>
        <p class="c_summary">{{ chapter.chapter_summary }}</p>
        <p class="verses_count">Verses: {{ chapter.verses_count }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chapters: [],
    };
  },
  async mounted() {
    await this.getData();
  },
  methods: {
    async getData() {
      const url = 'https://bhagavad-gita3.p.rapidapi.com/v2/chapters/?limit=18';
      const options = {
        method: 'GET',
        headers: {
          'X-RapidAPI-Key': 'f8c08f1481msh4f272c4e9b101bdp127ca0jsn38bed71f62c7',
          'X-RapidAPI-Host': 'bhagavad-gita3.p.rapidapi.com',
        },
      };

      try {
        const response = await fetch(url, options);
        const data = await response.json();

        this.chapters = data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
