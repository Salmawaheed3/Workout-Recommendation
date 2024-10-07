
# FitnessModel Documentation

## Overview
The `FitnessModel` class provides recommendations for personalized fitness plans and workouts. It utilizes clustering classification and other machine learning techniques to generate dynamic workout plans based on user details like goals, fitness level, gender, etc.

## Initialization
### FitnessModel
Initializes the model by loading the necessary data and pre-trained machine learning models.

```python
FitnessModel(excercise_path, kmeans_path, plan_classifier_path)
```

**Arguments:**
- `excercise_path` (string): Path to the CSV file containing exercise details.
- `kmeans_path` (string): Path to the pickled KMeans model.
- `plan_classifier_path` (string): Path to the pickled plan classifier model.

**Returns:**  
`FitnessModel` object.

## Methods

### choose_plan
Predicts a 30-day workout plan based on the input parameters using the pre-trained plan classifier model (RandomForest model).

```python
choose_plan(self, level, goal, gender)
```

**Arguments:**
- `level` (string): Fitness level - 'Beginner', 'Intermediate', or 'Advanced'.
- `goal` (string): Workout goal - 'Lose Weight', 'Gain Muscle', or 'Get Fitter'.
- `gender` (string): User's gender - 'Male' or 'Female'.

**Returns:**  
List of lists containing body parts for each day plan.

**Example:**
```python
plan = fitness_model.choose_plan('Intermediate', 'Lose Weight', 'Female')
```

### get_daily_recommendation
Predicts a cluster for each body part and selects random exercises from that cluster, filtering based on location and equipment availability (K-means model).

```python
get_daily_recommendation(self, home_or_gym, level, goal, bodyParts, equipments)
```

**Arguments:**
- `home_or_gym` (int): 0 for home, 1 for gym.
- `level` (string): Fitness level.
- `goal` (string): Workout goal.
- `bodyParts` (list): List of body parts to target (the output of `choose_plan` method).
- `equipments` (list): List of equipment ['band', 'dumbbell', 'body weight', 'Exercise Ball', 'Foam Roll', 'bosu ball', 'wheel roller', 'tire'].

**Returns:**  
List of exercise recommendations for the day.

**Example:**
```python
daily_recommendations = fitness_model.get_daily_recommendation(1, 'Beginner', 'Gain Muscle', ['Chest', 'Back'], ['Dumbbells'])
```

### adjust_workout
Calculates the new adjusted weight for an exercise based on user attributes, previous weight, and feedback.

```python
adjust_workout(self, gender, age, feedback, body_part, level, old_weight)
```

**Arguments:**
- `gender` (string): User's gender.
- `age` (int): User's age.
- `feedback` (bool): Positive feedback from previous workouts - True or False.
- `body_part` (string): Body part to target.
- `level` (string): Fitness level.
- `old_weight` (float): Previous workout weight.

### calculate_new_repetition
Calculates the suggested number of repetitions based on fitness level and goal.

```python
calculate_new_repetition(self, level, goal)
```

**Arguments:**
- `level` (string): Fitness level.
- `goal` (string): Workout goal.

### calculate_new_duration
Calculates the suggested exercise duration in seconds based on fitness level.

```python
calculate_new_duration(self, level)
```

**Arguments:**
- `level` (string): Fitness level.

### get_gender_adjustment
Returns a float adjustment value (0.7 or 1.0) based on the user's gender to scale workout intensities differently for males vs females.

```python
get_gender_adjustment(self, gender)
```

**Arguments:**
- `gender` (string): User's gender.

### get_age_adjustment
Returns an adjustment value between 0.1-1.0 based on the user's age to scale workout intensities accounting for age-related changes in abilities.

```python
get_age_adjustment(self, age)
```

**Arguments:**
- `age` (int): User's age.

### get_level_adjustment
Returns an adjustment value between 0.8-1.2 based on the user's fitness level to scale intensities appropriately for their experience level.

```python
get_level_adjustment(self, level)
```

**Arguments:**
- `level` (string): Fitness level.

### get_body_part_adjustment
Returns an adjustment value between 0.5-1.0 based on the targeted body part to scale intensities for different muscle groups.

```python
get_body_part_adjustment(self, body_part)
```

**Arguments:**
- `body_part` (string): Body part to target.

### encode_features
Performs one-hot encoding on categorical features to prepare the data for modeling.

```python
encode_features(self, features)
```

**Arguments:**
- `features` (list): List of features to encode.

**Returns:**  
Encoded features.

## Predict
Generates a full 30-day customized workout plan by predicting daily body parts, selecting exercises, and adjusting sets/reps/weights for each user.

```python
predict(self, home_or_gym, level, goal, gender, age, feedback, old_weight, equipments)
```

**Arguments:**
- `home_or_gym` (int): 0 for home, 1 for gym.
- `level` (string): Fitness level - 'Beginner', 'Intermediate', or 'Advanced'.
- `goal` (string): Workout goal - 'Lose Weight', 'Gain Muscle', or 'Get Fitter'.
- `gender` (string): User's gender - 'Male' or 'Female'.
- `age` (int): User's age.
- `feedback` (bool): Positive feedback from previous workouts - True or False.
- `old_weight` (float): Previous workout weight.
- `equipments` (list): List of equipment ['band', 'dumbbell', 'body weight', 'Exercise Ball', 'Foam Roll', 'bosu ball', 'wheel roller', 'tire'].

**Returns:**  
List of lists containing recommended exercises for each day of the 30-day plan.

**Example:**
```python
recommendations = fitness_model.predict(1, 'Advanced', 'Gain Muscle', 'Male', 22, True, 5, ['band', 'dumbbell'])
```
