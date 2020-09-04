<template>
<div id="app">
  <div class="container">
    <div class="row header-game">
      <div class="col-sm-6">
        <template v-if="index==0">
          <div style="float:left;position:absolute;">playing</div>
        </template>
        <h2>YOU</h2>
        <div class="progressb">
          <div class="progress" :style="'width:'+health.you+'%'">
            <p>{{health.you}} %</p>
          </div>
        </div>
      </div>
      <div class="col-sm-6">

        <h2>MONSTER</h2>

        <div class="progressb">
          <div class="progress" :style="'width:'+health.monster+'%'">
            <p>{{health.monster}} %</p>
          </div>
        </div>
        <template v-if="index==1">
          <div style="float:right; position:absolute; left:100%;top:10%;">playing</div>
        </template>
      </div>
    </div>
    <div class="menu">
      <button class="btn btn-success" @click="rungame" v-if="!isplaying">START GAME</button>
      <template v-else>
        <button class="btn btn-danger" @click="attack">ATTACK</button>
        <button class="btn btn-warning" @click="specialattack">SPECIAL ATTACK</button>
        <button class="btn btn-success" @click="heal">HEAL</button>
        <button class="btn btn-info" @click="isplaying=false">GIVE UP</button>
      </template>
    </div>

    <div class="container log-list">
      <div class="row">
        <div class="col-sm-12" v-for="(log,e) in history" :key="e">
          <p>{{log}}</p>
        </div>
      </div>
    </div>

  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isplaying: false,
      health: {
        you: 100,
        monster: 100
      },
      index: 0,
      history: []
    }
  },
  methods: {


    rungame: function() {

      this.health.you = 100;
      this.health.monster = 100;
      this.isplaying = true;
      this.history = [""];

    },

    attack: function() {


      if (this.index == 0) {
        if (!this.checkWinner()) {
          this.health.monster -= 5;
          this.index = 1;
          this.history.push("Player hits monster for 5%");

        }
        else{
return
        }
        return
      }
      else{
        if (!this.checkWinner()) {
          this.health.you -= 7;
          this.index = 0;
          this.history.push("Monster hits Player for 7%");

        }
        else{
return
        }
      }
    },
    specialattack: function() {
      if (this.index == 0) {
        this.health.monster -= 8;
        this.index = 1;
        this.history.push("Player hits monster for 8%");
      } else {
        this.health.you -= 8;
        this.index = 0;
        this.history.push("Monster hits player for 8%");
      }
    },

    heal: function() {
      if (this.index == 0) {
        if (this.health.you <= 95) {
          this.health.you += 5;
          this.index = 1;
          this.history.push("Player heals 5%");
        } else {
          this.index = 1;
        }

      } else if (this.health.monster <= 95) {
        this.health.monster += 5;
        this.index = 0;
        this.history.push("monster hits 5%");
      } else {
        this.index = 0;
      }


    },

    checkWinner: function() {
      if (this.health.monster <= 0) {
        if (confirm("You won ! | New Game?")) {
          this.rungame();
        } else {
          this.isplaying = false;

        }
        return true;
      } else if (this.health.you <= 0) {
        if (confirm("Monster won ! | New Game?")) {
          this.rungame();
        } else {
          this.isplaying = false;
        }
        return true;
      }
      return false;

    },

    healbutton: function() {}
  },
  watch: {
    health: {
      // This will let Vue know to look inside the array


      // We have to move our method to a handler field
      you(health) {
        console.log('The list of colours has changed!' + health)
      }
    }
  },

  components: {

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.header-game {
  margin-bottom: 40px;
}

.progressb {
  width: 200px;
  height: 30px;
  margin: 0 auto;

  padding: 0px;
  background-color: #c8c7c5;

}

.progressb p {
  margin: 0 auto;

  color: #f3f3f3;


  font-weight: 700;
  text-align: center;
}

.progress {
  background-color: #378b10;
  width: 100%;
  height: 30px;
  transition: 1s;

}

.menu {
  display: flex;
  border: 1px solid grey;
  padding: 15px;
  box-shadow: 2px 5px #cbcbcb;

  justify-content: space-around;
}

.menu button {}

.log-list {
  padding: 20px;

}

.log-list div:nth-child(even) {
  background-color: #6ba4b6;
}
</style>
