<template>

    <div>
        <h1>Reservix-Clicker</h1>

        <div class="container">

            <div class="score">
                <p><strong>Score:</strong> {{ score / scoreReducer }} {{ scoreReducer > 1 ? 'M' : ''}}</p>
                <p><strong>High-Score:</strong> {{ highscore / scoreReducer }} {{ scoreReducer > 1 ? 'M' : ''}}</p>
                <p><strong>Multiplicator:</strong> {{ multiplicator / scoreReducer }} {{ scoreReducer > 1 ? 'M' : ''}}</p>
            </div>

            <div class="clickelement" @click="updateScore()">
                <img src="./../assets/facebookLogo.png" alt="" style="width: 100%">
            </div>

            <div class="actions">
                <p>x2</p>
                <div class="progress" :style="{ width: updateProgress(1) + '%'}">{{ updateProgress(1) }} %</div>
                <div class="btn">
                    <button v-show="(score >= 100 * multiplicator)" type="button" name="double" @click="buymulti(2)">x2</button>
                </div>
                <p>x4</p>
                <div class="progress" :style="{ width: updateProgress(4) + '%'}">{{ updateProgress(4) }} %</div>
                <div class="btn">
                    <button v-show="score >= 400 * multiplicator" type="button" name="quad" @click="buymulti(4)">x4</button>
                </div>

            </div>

            <div class="clearfix"></div>
        </div>

    </div>

</template>

<script>
export default {
  name: 'Clicker',
  data() {
      return {
          score: 0,
          highscore: 0,
          scoreReducer: 1,
          multiplicator: 1
      }
  },
  methods : {
      /**
       * @name buymulti
       * @param mulit {number}
       * @desc buying a multiplicator x2
       **/
      buymulti(multi) {
          this.score -= 100 * this.multiplicator;
          this.multiplicator *= multi;
          this.updateProgress(multi);
      },
      /**
       * @name updateScore
       * @desc updating the score call highscore
       **/
      updateScore() {
          this.score += 1 * this.multiplicator;
          this.updateHighScore();
          this.cutScore();
      },
      /**
       * @name updateHighScore
       * @desc updating the highscore
       **/
      updateHighScore() {
          if (this.score >= this.highscore) {
              this.highscore = this.score;
          }
      },
      /**
       * @name updateProgress
       * @param value {number}
       * @return number
       * @desc updateing the progress bar
       **/
      updateProgress(value) {
          return Math.round((((this.score * 100) / 100) - ((100 * this.multiplicator * value) / 100 )) / this.multiplicator / value);
      },
      /**
       * @name cutScore
       * @desc divides score by 1m to make it more readable
       **/
      cutScore() {
          if (this.score > 1000000) {
              this.scoreReducer = 1000000;
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    font-family: sans-serif;
}

.container {

    width: 1000px;
    margin: 0 auto;

    .score {
        width: 950px;
        text-align: center;
        background-color: rgb(80,80,80);
        padding: 25px;
        p {
            color: white;
            font-size: 22px;
            line-height: 1.4em;
        }
    }

    .clickelement {
        width: 500px;
        height: 500px;
        float: left;
        background-color: red;
    }

    .actions {
        float: left;
        background-color: rgb(120,120,120);
        width: 450px;
        height: 500px;
        padding: 25px;

        .progress {
            width: 0%;
            max-width: 100%;
            height: 20px;
            background-color: green;
            color: white;
            line-height:0;
        }
        .btn {
            height: 50px;

            button {
                background-color: rgb(0,120,250);
                padding: 10px;
                border: none;
                color: white;
                font-size: 22px;
                &:hover {
                    background-color: rgb(0,140,255);
                }
            }
        }

    }

}





.clearfix {
    clear: both;
    float: none;
}

</style>
