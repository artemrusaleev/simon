<template>
  <div class="wrapper">
    <h1>Simon Says</h1>
    <div class="game-board">
      <div class="simon">
        <ul>
          <li
            class="tile red"
            v-bind:style="{ background: red }"
            @click="clickOnRedArea"
          ></li>
          <li
            class="tile blue"
            v-bind:style="{ background: blue }"
            @click="clickOnBlueArea"
          ></li>
          <li
            class="tile yellow"
            v-bind:style="{ background: yellow }"
            @click="clickOnYellowArea"
          ></li>
          <li
            class="tile green"
            v-bind:style="{ background: green }"
            @click="clickOnGreenArea"
          ></li>
        </ul>
      </div>
    </div>
    <div class="game-info">
      <h2>Раунд: {{ round }}</h2>
      <button @click="init">Старт</button>
    </div>
    <div class="game-options">
      <h2>Опции:</h2>
      <input type="radio" v-model="level" value="1500" checked />Легкий<br />
      <input type="radio" v-model="level" value="1000" />Средний<br />
      <input type="radio" v-model="level" value="400" />Сложный<br />
    </div>
    <div data-action="sound"></div>
  </div>
</template>

<script>
export default {
  name: "Game",
  data: () => ({
    gameSteps: [],
    userSteps: [],
    level: 1500,
    round: undefined,
    isWin: undefined,
    isSuccessStep: undefined,
    idOfInterval: undefined,
    isStrict: true,
    isUpdateOneOfColors: undefined,
    numOfStep: undefined,
    buttonsIsActive: true,
    sound: true,
    switchingOnСounter: undefined,
    red: "darkred",
    blue: "darkblue",
    green: "darkgreen",
    yellow: "goldenrod",
    redSound: new Audio(require("@/assets/sounds/1.mp3")),
    blueSound: new Audio(require("@/assets/sounds/2.mp3")),
    greenSound: new Audio(require("@/assets/sounds/3.mp3")),
    yellowSound: new Audio(require("@/assets/sounds/4.mp3")),
  }),
  methods: {
    init() {
      (this.buttonsIsActive || this.isWin) && this.start();
    },
    start() {
      this.gameSteps = [];
      this.userSteps = [];
      this.isWin = false;
      this.isSuccessStep = true;
      this.idOfInterval = 0;
      this.buttonsIsActive = true;
      this.switchingOnСounter = 0;
      this.numOfStep = 1;
      this.round = 1;
      for (let i = 0; i < 20; i += 1) {
        this.gameSteps.push(Math.floor(Math.random() * 4) + 1);
      }
      this.isUpdateOneOfColors = true;
      this.idOfInterval = setInterval(this.goToNextArea, this.level);
    },
    backToDefaultColors() {
      this.red = "darkred";
      this.blue = "darkblue";
      this.green = "darkgreen";
      this.yellow = "goldenrod";
    },
    goToNextArea() {
      this.buttonsIsActive = false;
      if (this.switchingOnСounter === this.numOfStep) {
        clearInterval(this.idOfInterval);
        this.isUpdateOneOfColors = false;
        this.backToDefaultColors();
        this.buttonsIsActive = true;
      }
      if (this.isUpdateOneOfColors) {
        this.backToDefaultColors();
        setTimeout(() => {
          switch (this.gameSteps[this.switchingOnСounter]) {
            case 1:
              this.updateBlue();
              break;
            case 2:
              this.updateRed();
              break;
            case 3:
              this.updateYellow();
              break;
            case 4:
              this.updateGreen();
              break;
          }
          this.switchingOnСounter += 1;
        }, 200);
      }
    },
    updateRed() {
      if (this.sound) this.redSound.play();
      this.sound = true;
      this.red = "tomato";
    },
    updateBlue() {
      if (this.sound) this.blueSound.play();
      this.sound = true;
      this.blue = "lightskyblue";
    },
    updateGreen() {
      if (this.sound) this.greenSound.play();
      this.sound = true;
      this.green = "lightgreen";
    },
    updateYellow() {
      if (this.sound) this.yellowSound.play();
      this.sound = true;
      this.yellow = "yellow";
    },
    winGame() {
      this.updateAllColors();
      this.round = "Победа";
      this.isWin = true;
    },
    updateAllColors() {
      this.red = "tomato";
      this.blue = "lightskyblue";
      this.green = "lightgreen";
      this.yellow = "yellow";
    },
    checkСorrectness() {
      if (
        this.userSteps[this.userSteps.length - 1] !==
        this.gameSteps[this.userSteps.length - 1]
      ) {
        this.isSuccessStep = false;
      }
      if (this.userSteps.length === 20 && this.isSuccessStep) this.winGame();
      if (!this.isSuccessStep) {
        this.updateAllColors();
        this.round = "Поражение";
        setTimeout(() => {
          this.round = this.numOfStep;
          this.backToDefaultColors();
          if (this.isStrict) {
            this.start();
          } else {
            this.isUpdateOneOfColors = true;
            this.switchingOnСounter = 0;
            this.userSteps = [];
            this.isSuccessStep = true;
            this.idOfInterval = setInterval(this.goToNextArea, this.level);
          }
        }, 800);
        this.sound = false;
      }
      if (
        this.numOfStep === this.userSteps.length &&
        this.isSuccessStep &&
        !this.isWin
      ) {
        this.numOfStep += 1;
        this.userSteps = [];
        this.isUpdateOneOfColors = true;
        this.switchingOnСounter = 0;
        this.round = this.numOfStep;
        this.idOfInterval = setInterval(this.goToNextArea, this.level);
      }
    },
    clickOnRedArea() {
      if (this.buttonsIsActive) {
        this.userSteps.push(2);
        this.checkСorrectness();
        this.updateRed();
        if (!this.isWin) {
          setTimeout(() => {
            this.backToDefaultColors();
          }, 50);
        }
      }
    },
    clickOnBlueArea() {
      if (this.buttonsIsActive) {
        this.userSteps.push(1);
        this.checkСorrectness();
        this.updateBlue();
        if (!this.isWin) {
          setTimeout(() => {
            this.backToDefaultColors();
          }, 50);
        }
      }
    },
    clickOnGreenArea() {
      if (this.buttonsIsActive) {
        this.userSteps.push(4);
        this.checkСorrectness();
        this.updateGreen();
        if (!this.isWin) {
          setTimeout(() => {
            this.backToDefaultColors();
          }, 50);
        }
      }
    },
    clickOnYellowArea() {
      if (this.buttonsIsActive) {
        this.userSteps.push(3);
        this.checkСorrectness();
        this.updateYellow();
        if (!this.isWin) {
          setTimeout(() => {
            this.backToDefaultColors();
          }, 50);
        }
      }
    },
  },
};
</script>
