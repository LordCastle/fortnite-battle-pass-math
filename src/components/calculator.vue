<template>
    <div class="calculator">
        <h1>Fortnite Season Pass Math</h1>

        <p>
            Update the fields below to calculate how many levels per day you
            need to max out your Fortnite season pass before it ends!
        </p>

        <p>
            Simply plug in your current level, and adjust the max level and
            season end date as you see fit. Fields automatically update when you
            change them.
        </p>

        <form class="form-container">
            <fieldset>
                <label for="">Your current level:</label>
                <input
                    type="number"
                    name="Your Level"
                    id="yourLevel"
                    min="0"
                    max="100"
                    v-model="userLevel"
                    v-on:input="calcLevelsNeeded"
                    title="min: 0, max: 100"
                />
            </fieldset>

            <fieldset>
                <label for="">Max level:</label>
                <input
                    type="number"
                    name="Maximum level"
                    id="maxLevel"
                    min="0"
                    max="100"
                    v-model="maxLevel"
                    v-on:input="calcLevelsNeeded"
                    title="min: 0, max: 100"
                />
            </fieldset>

            <fieldset>
                <label for="">Season End:</label>
                <date-picker
                    v-model="endDate"
                    format="MM-DD-YYYY"
                    v-on:input="calcLevelsNeeded"
                >
                </date-picker>
            </fieldset>
        </form>

        <div class="result">
            <p>
                There are <strong>{{ daysRemaining }}</strong> days remaining
                this season.
            </p>
            <p>
                You need to earn <strong>{{ levelsPerDay }}</strong> levels
                every day to max out the battle pass in Fornite before it ends.
            </p>
        </div>
    </div>
</template>

<script>
import DatePicker from "vue2-datepicker";
import "vue2-datepicker/index.css";

export default {
    name: "calcuator",
    components: { DatePicker },
    props: {},
    mounted() {
        this.calcLevelsNeeded();
    },
    methods: {
        calcLevelsNeeded() {
            let timeDifference =
                this.endDate.getTime() - this.todaysDate.getTime();
            this.daysRemaining = timeDifference / (1000 * 3600 * 24);

            this.levelsPerDay = Math.round(
                (this.maxLevel - this.userLevel) / this.daysRemaining
            );
        }
    },
    data() {
        return {
            endDate: new Date([2021, 3, 15]),
            todaysDate: new Date(),
            userLevel: 0,
            maxLevel: 100,
            daysRemaining: null,
            levelsPerDay: null
        };
    }
};
</script>

<style lang="scss" scoped>
.calculator {
    max-width: 400px;
    margin: 2rem auto;

    .form-container {
        display: flex;
        flex-direction: column;

        fieldset {
            flex: 1 1 calc(100% / 3);
            margin: 0 0 1rem;
            padding: 1rem;

            @media screen and (min-width: 768px) {
                margin: 0 0.5rem 1rem;
            }
        } // fieldset

        label {
            display: block;
            font-weight: 600;
            margin: 0 0 0.25em;
        }

        input {
            text-align: center !important;

            &[type="number"] {
                border: 1px solid #ccc;
                border-radius: 4px;
                box-shadow: inset 0 1px 1px rgba(black, 0.08);
                color: #555;
                display: inline-block;
                height: 34px;
                font-size: 14px;
                max-width: 120px;
                padding: 6px 10px;
                width: 100%;
            }
        } // input

        .mx-datepicker {
            max-width: 120px;
            width: 100%;

            .mx-input {
                text-align: center;
            }
        } // .mx-datepicker

        @media screen and (min-width: 768px) {
            flex-direction: row;
        }
    } // .form-container

    @media screen and (min-width: 768px) {
        max-width: 800px;
    }
} // .calculator
</style>
