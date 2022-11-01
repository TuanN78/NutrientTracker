# NutrientTracker
testing

from dataclasses import dataclass

import numpy as np
import matplotlib.pyplot as plt

calorie_goal = 3000
protein_goal = 180
fats_goal = 97
carbs_goal = 300

today = []

@dataclass
class Food:
    name: str
    calories: int
    protein: int
    fats: int
    carbs: int

done = False

while not done:
    print("""
    (1) Add a new food
    (2) Visuale progress
    (q) Quit
    """)

    choice = input("Choose an option: ")

    if choice == "1":
        print("Adding a new food! ")
        name = input("name: ")
        calories = int(input("Calories: "))
        proteins = int(input("Proteins: "))
        fats = int(input("Fats: "))
        carbs = int(input("Carbs: "))
        food = Food(name, calories, proteins, fats, carbs)
        today.append(food)
        print("Successfully added! ")
    elif choice == '2':
        calorie_sum = sum(food.calories for food in today)
        protein_sum = sum(food.protein for food in today)
        fats_sum = sum(food.fats for food in today)
        carbs_sum = sum(food.carbs for food in today)

        fig, axs = plt.subplots(5,2)
        axs[0, 0].pie([protein_sum, fats_sum, carbs_sum], labels=["Proteins", "Fats", "Carbs"], autopct="%1.1f%%")
        axs[0, 0].set_title("Macronutrients Distribution")

        axs[0, 1].bar([0, 1, 2], [protein_sum, fats_sum, carbs_sum], width = 0.4)
        axs[0, 1].bar([0.5, 1.5, 2.5], [protein_goal, fats_goal, carbs_goal], width = 0.4)
        axs[0, 1].set_title("Macronutrients Progress")

        axs[1, 0].pie([calorie_sum, calorie_goal - calorie_sum], labels=["Calories", "Remaining"], autopct="%1f%%")
        axs[1, 0].set_title("Calorie Goal Progress")

        axs[1, 1].plot(list(range(len(today))), np.cumsum([food.calories for food in today]), label=["Calories Eaten"])
        axs[1, 1].plot(list(range(len(today))), [calorie_goal] * len(today), label="Calorie Goal")
        axs[1, 1].legend()
        axs[1, 1].set_title("Calories Goal Over Time")

        axs[2, 0].pie([protein_sum, protein_goal - protein_sum], labels=["Proteins", "Remaining"], autopct="%1f%%")
        axs[2, 0].set_title("Protein Goal Progress")

        axs[2, 1].plot(list(range(len(today))), np.cumsum([food.protein for food in today]), label=["Protein Eaten"])
        axs[2, 1].plot(list(range(len(today))), [protein_goal] * len(today), label="Protein Goal")
        axs[2, 1].legend()
        axs[2, 1].set_title("Protein Goal Over Time")

        axs[3, 0].pie([fats_sum, fats_goal - fats_sum], labels=["Fats", "Remaining"], autopct="%1f%%")
        axs[3, 0].set_title("Fats Goal Progress")

        axs[3, 1].plot(list(range(len(today))), np.cumsum([food.fats for food in today]), label=["Fats Eaten"])
        axs[3, 1].plot(list(range(len(today))), [fats_goal] * len(today), label="Fats Goal")
        axs[3, 1].legend()
        axs[3, 1].set_title("Fats Goal Over Time")

        axs[4, 0].pie([carbs_sum, carbs_goal - carbs_sum], labels=["Carbs", "Remaining"], autopct="%1f%%")
        axs[4, 0].set_title("Carbs Goal Progress")

        axs[4, 1].plot(list(range(len(today))), np.cumsum([food.carbs for food in today]), label=["Carbs Eaten"])
        axs[4, 1].plot(list(range(len(today))), [carbs_goal] * len(today), label="Carbs Goal")
        axs[4, 1].legend()
        axs[4, 1].set_title("Carbs Goal Over Time")

        fig.tight_layout()
        plt.show()
    elif choice == "q":
        done = True
    else:
        print("Invalid choice")