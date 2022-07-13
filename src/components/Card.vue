<template>
  <div v-cloak>
    <h1>Attendance Count App</h1>

    <div class="container">
      <div class="card" v-for="(count,nameOfPerson) in countName" :key="nameOfPerson">
        <h1 class="name">{{ nameOfPerson }}</h1>
        <div class="count" id="counted">{{ count }}</div>
      </div>
      <!-- <h1 class="name">{{ name.toUpperCase() }}</h1>
      <div class="count" id="counted">{{ countNumber }}</div> -->
    </div>
    <div class="inputStuff">
      <input
        type="text"
        v-model="inputValue"
        placeholder="Please enter an a name"
      />
      <span><button @click="clicked">Enter</button></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counterName: "",
      name: "",
      inputValue: "",
      countNumber: 0,
    };
  },
  computed: {
    named() {
      let name = this.$store.state.names;
      console.log(name);
      return name;
    },
    countName() {
      const counter = {};

      const upper = this.$store.state.names.map((element) => {
        return element.toUpperCase();
      });

      // console.log(upper)

      upper.forEach((element) => {
        let currentCount = counter[element];
        if (currentCount) {
          counter[element] = currentCount + 1;
          // this.countNumber = currentCount + 1;
        } else {
          counter[element] = 1;
          // this.countNumber = 1;
        }
      });
      console.log(counter);

      return counter;
    },
  },
  methods: {
    clicked() {
      this.inputValue.trim();
      if (this.inputValue.length === 0) return;

      this.$store.state.names.push(this.inputValue.trim().toUpperCase());
      // console.log(this.$store.state.names)
      // console.log(this.inputValue)

      this.name = this.inputValue;
      this.inputValue = '';
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  font-family: "Edu NSW ACT Foundation", cursive;
}

.container{
  display: flex;
  flex-wrap: wrap;
}
.card {
  background: #2f2f2f;
  border: 4px solid #c39a3b;
  box-shadow: 3px 5px 7px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  width: 250px;
  Height: 90px;
  text-align: center;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin-right: auto;
  margin-left: auto;
  padding-bottom: 20px;
}

.name {
  color: white;
}

.count {
  color: white;
}

.inputStuff {
  text-align: center;
}

input {
  padding: 10px 15px;
}

button {
  padding: 10px 15px;
  border-radius: 4px;
  font-family: "Edu NSW ACT Foundation", cursive;
}

button:hover {
  background-color: #4caf50; /* Green */
  color: white;
}

[v-cloak] {
  display: none;
}
</style>
