
# Workout Plan Generator

This repository provides a system that generates customized workout plans and exposes a Flask-based API to retrieve exercise recommendations based on user input.

## Project Structure

1. **Data Processing**
   - The dataset of workout plans is processed and transformed into a CSV file.
   - It includes multiple exercises, specifying the name, type, equipment, body part targeted, sets, and repetitions.
   
2. **Flask API**
   - A lightweight Flask API is available to serve workout recommendations based on a set of input parameters provided by the user.

## Notebook Contents

The Jupyter Notebook covers two major components:

### 1. Workout Plans Dataset:
   - A list of recommended exercises grouped by days.
   - Each exercise includes attributes like:
     - `name`: Name of the exercise (e.g., Barbell Curl).
     - `type`: Type of the exercise (e.g., weight or duration-based).
     - `equipment`: Equipment needed (e.g., dumbbells, kettlebell).
     - `bodyPart`: The target muscle group (e.g., shoulders, legs).
     - `sets`: Number of sets to perform.
     - `repetitions`: Number of repetitions or duration for the exercise.
   - The final dataset is saved as a CSV file `plans.csv`.

### 2. Flask API:
   - **Route:** `POST /get_recommendations`
   - **Request Body:** JSON format with the following parameters:
     - `home_or_gym`: Location of the workout (e.g., Home, Gym).
     - `level`: User's fitness level (e.g., Beginner, Intermediate).
     - `goal`: Fitness goal (e.g., Gain muscle, Lose fat).
     - `gender`: User's gender.
     - `age`: User's age.
     - `feedback`: Feedback on previous workouts.
     - `old_weight`: Previous weight used for the exercise.
   - **Response:** A JSON object with personalized workout recommendations.

## How to Use

### 1. Data Processing:
- The notebook processes the raw workout plans dataset and saves the result as a CSV file (`plans.csv`). 
- Run the notebook to generate and save the processed workout plans locally.

### 2. Flask API:
To run the API server, execute the Flask app in the notebook:

```bash
python app.py
```

Once the server is running, you can test it using tools like `curl` or Postman:

#### Example Request:

```bash
curl -X POST http://127.0.0.1:5000/get_recommendations -H "Content-Type: application/json" -d '{
    "home_or_gym": "Gym",
    "level": "Intermediate",
    "goal": "Gain muscle",
    "gender": "Male",
    "age": 25,
    "feedback": "Good",
    "old_weight": 80
}'
```

The server will return recommendations tailored to the user's preferences and input data.

## Requirements

- Python 3.x
- Flask
- pandas (for data processing)

Install the required dependencies using pip:

```bash
pip install Flask pandas
```

## Running Locally

1. Clone the repository:

   ```bash
   git clone https://github.com/your-repo/workout-plan-generator.git
   ```

2. Navigate to the project directory:

   ```bash
   cd workout-plan-generator
   ```

3. Run the notebook to generate the workout plans and Flask API.
