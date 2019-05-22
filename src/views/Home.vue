<template>
  <div class="home container">
    <h1>Welcome to the Tributes Picker</h1>
    <div class="row">
      <div class="col" v-for="team in masterList">
        <table class="table">
          <thead>
            <tr>
              <th>{{ team.name }}</th>
            </tr>
          </thead>
          <tbody>
            <div v-for="member in team.members">
              <tr>
                <td>
                  <input type="checkbox" v-bind:id="member" v-bind:value="member" v-model="team.currentList">
                  <label v-bind:for="member">{{ member }}</label>
                </td>
              </tr>
            </div>
          </tbody>
        </table>
      </div>
    </div>
    <button v-on:click="picker()">Pick The Tributes</button>
    <ul>
       <li v-for="tribute in tributes">{{ tribute }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      masterList: [
        {
          name: "Magic Scrum Bus",
          members: ["Mike", "Anthony", "Adam", "Jennifer"],
          currentList: ["Mike", "Anthony", "Adam", "Jennifer"]
        },
        {
          name: "Lumber Jax",
          members: ["Matt", "Chris", "Rich", "Bill"],
          currentList: ["Matt", "Chris", "Rich", "Bill"]
        },
        {
          name: "Mighty Morphins",
          members: ["Intesar", "Evan", "Ramiro", "Joe", "Neha"],
          currentList: ["Intesar", "Evan", "Ramiro", "Joe", "Neha"]
        },
        {
          name: "4Scrumpany",
          members: ["Troy", "Navya", "Farha"],
          currentList: ["Troy", "Navya", "Farha"]
        },
        {
          name: "Peace And Chill",
          members: ["Azat", "Barbora", "Ildar", "Patrik", "Nour", "Stepan"],
          currentList: ["Azat", "Barbora", "Ildar", "Patrik", "Nour", "Stepan"]
        }
      ],
      tributes: []
    };
  },
  created: () => {},
  methods: {
    picker: function() {
      this.tributes = [];
      this.masterList.forEach(member => {
        const randNum = Math.floor(Math.random() * member.currentList.length);
        this.tributes.push(member.currentList[randNum]);
      });
    }
  }
};
</script>
