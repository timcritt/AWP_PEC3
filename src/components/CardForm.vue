<script>
export default {
  name: 'CardForm',
  data() {
    return {

    };
  }
}
</script>

<template>
  <section class="section-add">
    <button class="section-add__close">
      <img src="/src/assets/arrow-right.svg" alt="Close" />
    </button>
    <h2>Add a new show</h2>
    <form class="form">
      <div class="form-group">
        <label for="title">Title:</label>
        <input type="text" id="title" />
      </div>
      <div class="form-group">
        <label for="description">Description:</label>
        <textarea id="description"></textarea>
      </div>
      <div class="form-group">
        <label for="image">Image URL:</label>
        <input type="text" id="image" />
      </div>
      <div class="form-group">
        <label for="rating">Rating:</label>
        <input type="number" id="rating" />
      </div>
      <div class="form-group">
        <label for="tags">Tags:</label>
        <input type="text" id="tags" />
      </div>
      <div class="form-group">
        <label for="notes">Notes:</label>
        <textarea id="notes"></textarea>
      </div>
      <div class="form-group">
        <label for="color">Color:</label>
        <input type="color" id="color" />
      </div>
      <div class="form-group">
        <label for="releaseDate">Release date:</label>
        <input type="date" id="releaseDate" />
      </div>
      <button class="btn btn--cta" type="submit">Add show</button>
    </form>
  </section>
</template>

<style scoped>
/* Parent */
.section-add {
  width: calc(100% - 40px);
  min-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #393a41;
  color: white;
  position: relative;
}

.section-add__close {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: white;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  width: 20px;
  height: 20px;
}

/* Every item is wrapped in a form-group */
form {
  display: grid;
  gap: 10px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.form-group input,
.form-group textarea {
  width: 100%;
  box-sizing: border-box;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.form-group input[type="color"] {
  padding: 0;
  height: 40px;
}

.form-group textarea {
  resize: vertical;
}

.btn[type="submit"] {
  width: 100%;
}
</style>
