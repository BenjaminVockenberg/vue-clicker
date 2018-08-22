<template>

    <div>
        <h1>Reservix-Clicker</h1>

        <div class="container">

            <div class="score">
                <p><strong>Score:</strong> {{ score >= 1000000 ? (score / scoreReducer).toFixed(2) : score }} {{ score > 1000000 ? 'M' : ''}}</p>
                <p><strong>High-Score:</strong> {{ highscore >= 1000000 ? (highscore / scoreReducer).toFixed(2) : highscore }} {{ highscore > 1000000 ? 'M' : ''}}</p>
                <p><strong>Multiplicator:</strong> {{ score >= 1000000 ? (multiplicator / scoreReducer).toFixed(2) : multiplicator }} {{ score > 1000000 ? 'M' : ''}}</p>
            </div>

            <div class="clickelement" @click="updateScore()" :style="{ padding: paddingFactor + '%' }">
                <img src="./../assets/facebookLogo.png" alt="" style="width: 100%">
            </div>

            <div class="actions">

                <p>Multiplicator x2</p>
                <div class="progress_border">
                    <div class="progress" :style="{ width: updateProgress(1) + '%'}"></div>
                </div>
                <p>{{ updateProgress(1) }} %</p>
                <div class="btn">
                    <button v-show="(score >= 100 * multiplicator)" type="button" name="double" @click="buymulti(2)">x2</button>
                </div>

                <p>Multiplicator x4</p>
                <div class="progress_border">
                    <div class="progress" :style="{ width: updateProgress(4) + '%'}"></div>
                </div>
                <p>{{ updateProgress(4) }} %</p>
                <div class="btn">
                    <button v-show="score >= 400 * multiplicator" type="button" name="quad" @click="buymulti(4)">x4</button>
                </div>

                <p>Multiplicator x16</p>
                <div class="progress_border">
                    <div class="progress" :style="{ width: updateProgress(16) + '%'}"></div>
                </div>
                <p>{{ updateProgress(16) }} %</p>
                <div class="btn">
                    <button v-show="score >= 1600 * multiplicator" type="button" name="quad" @click="buymulti(16)">x16</button>
                </div>

                <p>Multiplicator x256</p>
                <div class="progress_border">
                    <div class="progress" :style="{ width: updateProgress(256) + '%'}"></div>
                </div>
                <p>{{ updateProgress(256) }} %</p>
                <div class="btn">
                    <button v-show="score >= 256000 * multiplicator" type="button" name="quad" @click="buymulti(256)">x256</button>
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
            paddingFactor: 0,
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
            if (this.score < 0) {
                this.score = 0;
            }
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
            this.updatePadding();
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
            return ((((this.score * 100) / 100) - ((100 * this.multiplicator * value) / 100 )) / this.multiplicator / value).toFixed(2) < 0 ? 0 :((((this.score * 100) / 100) - ((100 * this.multiplicator * value) / 100 )) / this.multiplicator / value).toFixed(2);
        },
        /**
        * @name cutScore
        * @desc divides score by 1m to make it more readable
        **/
        cutScore() {
            if (this.score > 1000000) {
                this.scoreReducer = 1000000;
            }
        },
        /**
        * @name updatePadding
        * @desc giving a visual feedback of clicking the clicker clickelement
        **/
        updatePadding() {
            this.paddingFactor += 1;
            if (this.paddingFactor >= 1) {
                setTimeout(() => {
                    this.paddingFactor = 0;
                }, 800);
            }
        }
    }
}
</script>

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
        padding: 0%;
        background-color: orange;
    }

    .actions {
        float: left;
        background-color: rgb(120,120,120);
        width: 450px;
        height: 500px;
        padding: 25px;

        .progress_border {
            width: 100%;
            background-color: rgb(80,80,80);
            .progress {
                width: 0%;
                max-width: 100%;
                height: 20px;
                background-color: green;
                color: white;
                line-height:0;
            }
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
