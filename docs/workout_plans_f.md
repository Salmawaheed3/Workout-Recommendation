
# Workout Plan Generator

This repository provides a system that generates customized workout plans.

## Project Structure

**Data Processing**
   - The dataset of workout plans is processed and transformed into a CSV file.
   - It includes multiple exercises, specifying the name, type, equipment, body part targeted, sets, and repetitions.
   
## Notebook Contents

The Jupyter Notebook covers two major components:

###  Workout Plans Dataset:
   - A list of recommended exercises grouped by days.
   - Each exercise includes attributes like:
     - `name`: Name of the exercise (e.g., Barbell Curl).
     - `type`: Type of the exercise (e.g., weight or duration-based).
     - `equipment`: Equipment needed (e.g., dumbbells, kettlebell).
     - `bodyPart`: The target muscle group (e.g., shoulders, legs).
     - `sets`: Number of sets to perform.
     - `repetitions`: Number of repetitions or duration for the exercise.
   - The final dataset is saved as a CSV file `plans.csv`.

## How to Use

### Data Processing:
- The notebook processes the raw workout plans dataset and saves the result as a CSV file (`plans.csv`). 
- Run the notebook to generate and save the processed workout plans locally.


