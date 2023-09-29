<template>
  <div class="search">
    <input v-model="searchQuery" class="search-input" placeholder="Search for keywords">
    <button @click="clearSearch" class="clear-button" v-show="searchQuery">X</button>
  </div>
  <div class="main">
    <div class="main-container">
      <div class="blog-heading">
        <h1>Hidden Valley Blog</h1>
      </div>
      <div class="about-other">
        <!-- Add a search input -->
        <div class="block">
          <div class="table-left">
            <ul class="main-text">
              <h3>October 2023</h3>
              <li class="main-li" v-for="(text, index) in mainText" :key="index">
                <span :class="{'highlight': isHighlighted(text)}">{{ text }}</span>
              </li>
            </ul>
          </div>
          <div class="main-right">
            <div class="main-opaque">
              <img class="about-img" src="../assets/blog.png" alt="Hidden Valley">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "", // Store the search query
      mainText: [
      "Hello everyone! I am so excited to be launching my new business running practical skills workshops at Hidden Valley. It is amazing how much I enjoy spending time in my garden these days. When I first started out gardening over 10 years ago, garden time was a list of jobs I needed to get done in order to produce cheap and healthy food. In my new No Dig garden I garden to centre and ground myself, and simply being in it makes me happy. And who would have thought compost making would become such an engaging hobby?! Instead of bringing in my garden inputs I now make great compost myself - a very satisfying process indeed.",
      "I have also been baking all of my family’s bread for the last 10 years - giving me plenty of time to develop an efficient method of baking artisan sourdough. I love giving them such delicious and nourishing bread, and they love eating it! I also really value the way bread baking is time spent being completely present and focused on the birth of the dough.",
      "When I am not gardening, baking or looking after the kids I am busy doing a building project around the house somewhere. I like being able to build exactly what I want, when I want to, without having to rely on others to do it for me. I am really excited to introduce more women to building tools and skills so that they can gain enough confidence and know-how to do their own building projects too.",
      "It will be great to share this special place with others, and I hope I can spread my enthusiasm for a more grounded way of life doing things for ourselves."

      ],
    };
  },
  computed: {
    // Compute the mainTextWithHighlights based on the searchQuery
    mainTextWithHighlights() {
      return this.mainText.map((text) => this.highlightSearchTerms(text, this.searchQuery));
    },
  },
  methods: {
    // Check if a text contains highlighted search terms
    isHighlighted(text) {
      if (!this.searchQuery) return false; // No search query, no highlighting

    // Find all occurrences of the searchQuery
      const regex = new RegExp(this.searchQuery, "gi");

      // Check if the text contains any matches
      return text.match(regex) !== null;
    },
    // Function to highlight search terms in text
    highlightSearchTerms(text, searchQuery) {
      if (!searchQuery) return text; // Return the original text if searchQuery is empty

      // Find all occurrences of the searchQuery
      const regex = new RegExp(searchQuery, "gi");

      // Replace the search term with a highlighted version
      return text.replace(regex, (match) => `<span class="highlight">${match}</span>`);
    },
    // Function to clear the search bar
    clearSearch() {
      this.searchQuery = "";
    },
  },
};
</script>

<style scoped>
/* Style for the search input */
.search {
  display: flex;
  justify-content: flex-end; /* Align the search input to the right */
  background-color: #186A3B; /* Background color to match the main container */
  background-color: rgba(255, 255, 255, 0.25); /* Background color with transparency */
}

.search-input {
  width: 140px;
  padding: 5px;
}

.clear-button {
  background-color: #186A3B; /* Background color for the button */
  color: white; /* Text color */
  border: none; /* Remove border */
  border-radius: 50%; /* Round button corners */
  padding: 5px 10px; /* Padding for button content */
  margin-left: 5px; /* Add some space between input and button */
  cursor: pointer; /* Change cursor to pointer on hover */
  display: flex; /* Align the button vertically with the input */
  align-items: center; /* Center button content vertically */
  font-size: 14px; /* Font size */
}

.clear-button:hover {
  background-color: #0a301b; /* Darker green on hover */
}

/* Styling for the blog heading section */
.blog-heading {
  width: 100%;
  display: flex;
  flex-direction: column; /* Stack content vertically */
  justify-content: space-between; /* Distribute content evenly */
  margin-bottom: 24px; /* Bottom margin for the heading section */
}

/* Additional styles for highlighting */
.highlight {
  background-color: #186A3B;
  color: white;
  font-weight: bold;
}
</style>