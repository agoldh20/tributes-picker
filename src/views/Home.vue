<template>
  <div class="home container">
    <h1>Welcome to the Tributes Picker</h1>
    <div class="row">
      <div class="col" v-for="(team, index) in masterList">
        <table class="table">
          <thead>
            <tr>
              <th>{{ team.name }} <span class="link" v-on:click="clearAll(index)">Deselect All</span></th>
            </tr>
          </thead>
          <tbody>
            <div v-for="member in team.members">
              <tr>
                <td>
                  <input type="checkbox" v-bind:id="member" v-bind:value="member" v-model="team.currentList">
                  <label v-bind:for="member">&nbsp;{{ member }}</label>
                </td>
              </tr>
            </div>
          </tbody>
        </table>
      </div>
    </div>
    <button v-on:click="picker()">Pick The Tributes</button>
    <ul>
       <li v-for="tribute in tributes">{{ tribute["team"] }}: {{ tribute["person"] }}</li>
    </ul>
  </div>
</template>
<style>
  .link {
    color: blue;
    font-size: small;
  }

  .link:hover {
    text-decoration: underline;
    cursor: pointer;
  }
</style>

<script>
export default {
  data: () => {
    return {
      masterList: [
        {
          name: "Prduct Owner",
          members: ["Allie", "Colleen", "Jess", "Marie", "Ryan"],
          currentList: ["Allie", "Colleen", "Jess", "Marie", "Ryan"]
        },
        {
          name: "Magic Scrum Bus",
          members: ["Adam", "Anthony", "Jennifer", "Mike"],
          currentList: ["Adam", "Anthony", "Jennifer", "Mike"]
        },
        {
          name: "Lumber Jax",
          members: ["Bill", "Chris", "Matt", "Hayes"],
          currentList: ["Bill", "Chris", "Matt", "Hayes"]
        },
        {
          name: "Mighty Morphins",
          members: ["Evan", "Intesar", "Joe", "Neha", "Ramiro"],
          currentList: ["Evan", "Intesar", "Joe", "Neha", "Ramiro"]
        },
        {
          name: "4Scrumpany",
          members: ["Farha", "Navya", "Troy"],
          currentList: ["Farha", "Navya", "Troy"]
        },
        {
          name: "Peace And Chill",
          members: ["Azat", "Barbora", "Ildar", "Nour", "Patrik", "Stepan"],
          currentList: ["Azat", "Barbora", "Ildar", "Nour", "Patrik", "Stepan"]
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
        let pick = {};
        const randNum = Math.floor(Math.random() * member.currentList.length);
        pick["team"] = member.name;
        pick["person"] = member.currentList[randNum];
        this.tributes.push(pick);
      });
    },
    clearAll: function(teamIndex) {
      this.masterList[teamIndex].currentList = [];
    }
  }
};
</script>
