<template>
  <div id="app">
        <header>
            <h1>MyFitness</h1>
        </header>
        <main>
            <section class="workout-section">
                <h2>Workout Tracking</h2>
                <div class="workout-form">
                    <input type="text" v-model="exerciseName" placeholder="Exercise Name">
                    <input type="number" v-model="sets" placeholder="Sets">
                    <input type="number" v-model="reps" placeholder="Reps">
                    <input type="number" v-model="weight" placeholder="Weight (kgs)">
                    <button @click="logWorkout">Log Workout</button>
                </div>
                <ul class="workout-list">
                    <li v-for="(workout, index) in workouts" :key="index">
                        {{ workout.exerciseName }} - Sets: {{ workout.sets }}, Reps: {{ workout.reps }}, Weight: {{ workout.weight }} kgs
                        <button @click="deleteWorkout(index)">Delete</button>
                    </li>
                </ul>
                <div class="chart">
                    <h3>Workout Progress Chart</h3>
                    <canvas id="workoutChart"></canvas>
                </div>
            </section>
            <section class="nutrition-section">
                <h2>Nutrition Tracking</h2>
                <div class="nutrition-form">
                    <input type="text" v-model="mealName" placeholder="Meal Name">
                    <input type="number" v-model="calories" placeholder="Calories">
                    <button @click="logMeal">Log Meal</button>
                </div>
                <ul class="meal-list">
                    <li v-for="(meal, index) in meals" :key="index">
                        {{ meal.mealName }} - Calories: {{ meal.calories }}
                        <button @click="deleteMeal(index)">Delete</button>
                    </li>
                </ul>
                <div class="chart">
                    <h3>Calories Consumed Chart</h3>
                    <canvas id="caloriesChart"></canvas>
                </div>
            </section>
        </main>
    </div>
</template>

<script>
export default {
  data() {
        return {
            exerciseName: '',
            sets: null,
            reps: null,
            weight: null,
            workouts: [],
            mealName: '',
            calories: null,
            meals: [],
        };
    },
    methods: {
        logWorkout() {
            if (!this.exerciseName || !this.sets || !this.reps || !this.weight) return;

            const workout = {
                exerciseName: this.exerciseName,
                sets: this.sets,
                reps: this.reps,
                weight: this.weight,
            };

            this.workouts.push(workout);
            this.resetWorkoutForm();

            // Update the workout progress chart
            this.updateWorkoutChart();
        },
        deleteWorkout(index) {
            this.workouts.splice(index, 1);
            this.updateWorkoutChart();
        },
        logMeal() {
            if (!this.mealName || !this.calories) return;

            const meal = {
                mealName: this.mealName,
                calories: this.calories,
            };

            this.meals.push(meal);
            this.resetMealForm();

            // Update the calories consumed chart
            this.updateCaloriesChart();
        },
        deleteMeal(index) {
            this.meals.splice(index, 1);
            this.updateCaloriesChart();
        },
        resetWorkoutForm() {
            this.exerciseName = '';
            this.sets = null;
            this.reps = null;
            this.weight = null;
        },
        resetMealForm() {
            this.mealName = '';
            this.calories = null;
        },
        updateWorkoutChart() {
            // code to update chart
        },
        updateCaloriesChart() {
            // code to update chart
        },
    },
};



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* Body styles */
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    color: #333;
}

/* Header styles */
header {
    background-color: #007BFF;
    color: white;
    text-align: center;
    padding: 1rem 0;
}

/* Main content styles */
main {
    max-width: 600px;
    margin: 2rem auto;
    padding: 1rem;
    background-color: white;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

/* Section styles */
.workout-section,
.nutrition-section {
    border: 1px solid #6CB2EB;
    padding: 1rem;
    margin-bottom: 1rem;
}

/* Heading styles */
.workout-section h2,
.nutrition-section h2 {
    color: #0056b3;
}

/* Form styles */
.workout-form,
.nutrition-form {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.workout-form input[type="text"],
.nutrition-form input[type="text"],
.workout-form input[type="number"],
.nutrition-form input[type="number"] {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
}

.workout-form button,
.nutrition-form button {
    background-color: #007BFF;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
}

/* List item styles */
.workout-list li,
.meal-list li {
    display: flex;
    align-items: center;
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
}

/* Chart styles */
.chart {
    background-color: white;
    border: 1px solid #6CB2EB;
    padding: 1rem;
    margin-bottom: 1rem;
}

.chart h3 {
    color: #0056b3;
}

</style>
