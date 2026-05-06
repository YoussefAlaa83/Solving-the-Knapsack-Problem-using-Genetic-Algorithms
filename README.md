# Solving-the-Knapsack-Problem-using-Genetic-Algorithms

For Code Implementation:

import random

items = [(10, 2), (20, 3), (30, 5), (40, 7)]
max_weight = 10

def calculate_fitness(chromosome):
    total_val = 0
    total_wt = 0
    for i in range(len(chromosome)):
        if chromosome[i] == 1:
            total_val += items[i][0]
            total_wt += items[i][1]
    
    return total_val if total_wt <= max_weight else 0


population = [[random.randint(0, 1) for _ in range(len(items))] for _ in range(10)]


for generation in range(50):
  
    population = sorted(population, key=lambda x: calculate_fitness(x), reverse=True)
    
    
    next_gen = population[:2]
    
    
    while len(next_gen) < 10:
        parent1, parent2 = random.sample(population[:5], 2)
        point = random.randint(1, len(items)-1)
        child = parent1[:point] + parent2[point:]
        
        if random.random() < 0.1: 
            idx = random.randint(0, len(items)-1)
            child[idx] = 1 - child[idx]
            
        next_gen.append(child)
    
    population = next_gen

best_solution = population[0]
print(f"Best Configuration: {best_solution}")
print(f"Total Value: {calculate_fitness(best_solution)}")
