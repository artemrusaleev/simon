<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from "./components/Game";
export default {
  name: "App",
  components: { Game },
};
</script>

<style lang="scss">
body {
  font-family: Arial, serif;
  color: black;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}
h1 {
  margin: 1em 0 2em;
  text-align: center;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  padding: 0;
  margin: 0;
}
p[data-action="lose"] {
  display: none;
}
.active {
  opacity: 1 !important;
}
.clearfix {
  width: 100%;
  clear: both;
}
.wrapper {
  width: 540px;
  margin: 0 auto;
}
.container {
  width: 305px;
}
.simon {
  background: #fff;
  position: relative;
  float: left;
  margin-right: 3em;
  width: 302px;
  height: 295px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  -moz-box-shadow: 2px 1px 12px #aaa;
  -webkit-box-shadow: 2px 1px 12px #aaa;
  -o-box-shadow: 2px 1px 12px #aaa;
  box-shadow: 2px 1px 12px #aaa;
}
.tile {
  opacity: 0.6;
  -webkit-transition: opacity 250ms ease;
  -moz-transition: opacity 250ms ease;
  -ms-transition: opacity 250ms ease;
  -o-transition: opacity 250ms ease;
  transition: opacity 250ms ease;
}
.tile.lit {
  opacity: 1;
}
.red {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
  clip: rect(0px, 300px, 150px, 150px);
  width: 296px;
  &:hover {
    border: 2px solid black;
  }
}
.blue {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
  clip: rect(0px, 150px, 150px, 0px);
  width: 300px;
  &:hover {
    border: 2px solid black;
  }
}
.yellow {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
  clip: rect(150px, 150px, 300px, 0px);
  width: 300px;
  &:hover {
    border: 2px solid black;
  }
}
.green {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
  clip: rect(150px, 300px, 300px, 150px);
  width: 296px;
  &:hover {
    border: 2px solid black;
  }
}
.game-info {
  margin-top: 90px;
  button {
    width: 5em;
    box-sizing: border-box;
    font-size: 1.4em;
    -webkit-border-radius: 10px 10px 10px 10px;
    border-radius: 10px 10px 10px 10px;
    background: #6dabe8;
    border: none;
    padding: 0.3em 0.6em;
    &:hover {
      background: #78bcff;
    }
  }
}
.game-options {
  h2 {
    margin-top: 30px;
    margin-bottom: 0;
  }
  input[type="radio"] {
    margin-right: 10px;
  }
}
.hoverable {
  &:hover {
    cursor: pointer;
  }
}
footer {
  position: absolute;
  bottom: 20px;
  width: 540px;
  clear: both;
  text-align: center;
}
</style>
