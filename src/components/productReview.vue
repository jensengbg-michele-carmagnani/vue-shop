 
 <template >
  <form class="review-form" @submit.prevent="onSubmit">
    <p>
      <label for="name">Name :</label>
      <input id="name" v-model="name" placeholder="name" />
    </p>
    <p>
      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
    </p>
    <p>
      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>
    <p>
      <input type="submit" value="Submit" />
    </p>
     <p v-if="errors.length">
    <b>Please correct the error(s):</b>
    <ul>
      <li v-for="(error, index) in errors" :key="index">{{error}}</li>
    </ul>

    </p>
  </form>
</template>
 
 <script>
export default {
  name: "productRevew",
  data() {
    return {
      name: null,
      review: null,
      rating: null,
      errors: [],
    };
  },
  methods: {
    onSubmit() {
      if (this.name && this.review && this.rating) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          
        };
        this.$emit("review-submitted", productReview);
        this.name = null;
        this.review = null;
        this.rating = null;
      } else {
        if (!this.name) this.errors.push("Name required");
        if (!this.review) this.errors.push("Review required");
        if (!this.rating) this.errors.push("Rating required");
      }
    },
  },
};
</script>
 
 <style>
.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;
}
</style>