<template>
  <div class="home container">
    <h1>Welcome to the Tributes Picker</h1>
    <div class="row">
      <div class="col" v-for="(team, index) in masterList">
        <table class="table">
          <thead>
            <tr>
              <th>{{ team.name }} <br>
                <span class="small-text">Select: </span><br>
                <span class="link" v-on:click="selectAll(index)">All</span> /
                <span class="link" v-on:click="clearAll(index)">Clear</span>
              </th>
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
    <ul style="padding-top: 10px;">
       <li v-for="tribute in tributes">{{ tribute["team"] }}: {{ tribute["person"] }}</li>
    </ul>
  </div>
</template>

<style>
.small-text {
  font-size: small;
}

.link {
  color: blue;
  font-size: small;
}

.link:hover {
  text-decoration: underline;
  cursor: pointer;
}

.col {
  padding-left: 5px;
  padding-right: 5px;
}
</style>

<script>
export default {
  data: () => {
    return {
      masterList: [
        {
          name: "Magic Scrum Bus",
          members: ["Adam", "Anthony", "Jennifer", "Mike"],
          currentList: ["Adam", "Anthony", "Jennifer", "Mike"]
        },
        {
          name: "Lumber Jax",
          members: ["Bill", "Matt", "Rich", "Stepan"],
          currentList: ["Bill", "Matt", "Rich", "Stepan"]
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
          members: ["Azat", "Barbora", "Ildar", "Nour", "Patrik"],
          currentList: ["Azat", "Barbora", "Ildar", "Nour", "Patrik"]
        },
        {
          name: "Pin Pals",
          members: ["Daniel C.", "Heney", "John", "Lenox"],
          currentList: ["Daniel C.", "Heney", "John", "Lenox"]
        },
        {
          name: "The Be Sharps",
          members: ["Daniel O.", "Diego", "Santiago N.", "Kelwin"],
          currentList: ["Daniel O.", "Diego", "Santiago N.", "Kelwin"]
        },
        {
          name: "Codevengers",
          members: ["Carlos", "Daniel M.", "Harry", "Santiago C."],
          currentList: ["Carlos", "Daniel M.", "Harry", "Santiago C."]
        },
        {
          name: "X-Force",
          members: ["Anthony", "Nicolas", "Katherina", "Juan"],
          currentList: ["Anthony", "Nicolas", "Katherina", "Juan"]
        }
      ],
      tributes: []
    };
  },
  created: () => {},
  methods: {
    picker: function() {
      const tempTribs = [];

      this.masterList.forEach(team => {
        if (team.currentList.length > 0) {
          let pick = {};
          const randNum = Math.floor(Math.random() * team.currentList.length);
          pick["team"] = team.name;
          pick["person"] = team.currentList[randNum];
          tempTribs.push(pick);
        }
      });

      while (tempTribs.length > 5) {
        tempTribs.splice(Math.floor(Math.random() * tempTribs.length), 1);
      }

      this.tributes = tempTribs;
      this.tributes.unshift({"team": "Forever Tributes", "person": "Stephen, Russ, Chris"});
    },
    clearAll: function(teamIndex) {
      this.masterList[teamIndex].currentList = [];
    },
    selectAll: function(teamIndex) {
      this.masterList[teamIndex].currentList = this.masterList[teamIndex].members;
    }
  }
};
</script>
