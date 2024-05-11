
<template>
  <div>
    <div class="form-container mt-5">
      <form @submit.prevent="saveData" class="form">
        <label for="postTitle"><strong>Post Title:</strong></label>
        <input id="postTitle" type="text" v-model="postData.postTitle">
        
        <label><strong>Category:</strong></label>
        <div class="checkbox-wrapper">
          <label v-for="category in categories" :key="category" class="checkbox-label">
            <input type="checkbox" :value="category" v-model="postData.category"> {{ category }}
          </label>
        </div>
        
        <label><strong>Series:</strong></label>
        <select v-model="postData.series">
          <option v-for="series in seriesOptions" :key="series" :value="series">{{ series }}</option>
        </select>
        
        <label><strong>Social Networks:</strong></label>
        <div class="checkbox-wrapper">
          <label v-for="network in socialNetworks" :key="network" class="checkbox-label">
            <input type="checkbox" :value="network" v-model="postData.socialNetworks"> {{ network }}
          </label>
        </div>
        
        <label>
          <input type="checkbox" v-model="postData.publishNow"> <strong>Publish Now:</strong>
        </label>
        
        <button type="submit" class="submit-btn btn-success">Next</button>
      </form>
    </div>
    
    <div class="display-data" v-if="submitted">
      <h2>User Data:</h2>
      <p><strong>Post Title:</strong> {{ postData.postTitle }}</p>
      <p><strong>Category:</strong> {{ formatArray(postData.category) }}</p>
      <p><strong>Series:</strong> {{ postData.series }}</p>
      <p><strong>Social Networks:</strong> {{ formatArray(postData.socialNetworks) }}</p>
      <p><strong>Publish Now:</strong> {{ postData.publishNow ? 'Yes' : 'No' }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      postData: {
        postTitle: "",
        category: [],
        series: "",
        socialNetworks: [],
        publishNow: false
      },
      categories: ["Web", "Network", "Backend", "Frontend", "UI&UX"],
      socialNetworks: ["Facebook", "Youtube", "Twitter", "Instagram"],
      seriesOptions: ["First", "Second", "Third"],
      submitted: false
    };
  },
  methods: {
    saveData() {
    
    //   console.log("Data saved:", this.postData);
      this.submitted = true; 
    },
    formatArray(arr) {
      return arr.length > 0 ? arr.join(", ") : "None";
    }
  }
};
</script>

<style scoped>
.form-container {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}

.form {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

label {
  display: block;
  margin-bottom: 10px;
}

input[type="text"],
select {
  width: 100%;
  padding: 8px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}

.checkbox-wrapper {
  display: flex;
  flex-wrap: wrap;
}

.checkbox-label,
.radio-label {
  margin-right: 20px;
}

.submit-btn {
  background-color: rgb(35, 122, 202);
  color: white;
  border: 1px solid rgb(35, 122, 202);
  border-radius: 5px;
  padding: 10px 20px;
  cursor: pointer;
}


.display-data {
  margin-top: 20px;
}
</style>
