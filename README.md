import pandas as pd 
import numpy as np 

data = pd.read_csv('lab1a.csv') 
concepts = np.array(data)[:, :-1] 
target = np.array(data)[:, -1] 

def train(con, tar): 
    for i, val in enumerate(tar): 
        if val == 'yes': 
            specific_h = con[i].copy() 
            break 

   for i, val in enumerate(con): 
        if tar[i] == 'yes': 
            for x in range(len(specific_h)): 
                if val[x] != specific_h[x]: 
                    specific_h[x] = '?' 
                else: 
                    pass 
    return specific_h 

print(train(concepts, target))


sky,airtemp,humidity,wind,water,forecast,enjoy sports 
sunny,warm,normal,strong,warm,same,yes 
sunny,warm,high,strong,warm,same,yes 
rainy,cold,high,strong,warm,change,no 
rainy,warm,high,light,cool,change,yes


import csv 

a = [] 
print("\nThe Given Training Data Set:\n") 
with open('ws.csv', 'r') as csvFile: 
    reader = csv.reader(csvFile) 
    for row in reader: 
        a.append(row) 
        print(row) 

num_attributes = len(a[0]) - 1  

S = ['0'] * num_attributes 
G = ['?'] * num_attributes 

print("\nThe initial value of hypothesis:") 
print("\nMost specific hypothesis S0 : [0,0,0,0,0,0]") 
print("Most general hypothesis G0 : [?,?,?,?,?,?]\n") 

for j in range(num_attributes): 
    S[j] = a[0][j] 

print("\nCandidate Elimination Algorithm – Hypothesis Version Space Computation\n") 
temp = [] 

for i in range(len(a)): 
    if a[i][num_attributes] == 'Yes': 
        for j in range(num_attributes): 
            if a[i][j] != S[j]: 
                S[j] = '?' 
        for j in range(num_attributes): 
            for k in range(len(temp)): 
                if temp[k][j] != '?' and temp[k][j] != S[j]: 
                    del temp[k] 
        print(f"For Training Example No : {i+1} the hypothesis is S{i+1}", S) 
        if len(temp) == 0: 
            print(f"For Training Example No : {i+1} the hypothesis is G{i+1}", G) 
        else: 
            print(f"For Training Example No : {i+1} the hypothesis is G{i+1}", temp) 
    if a[i][num_attributes] == 'No':  
        for j in range(num_attributes): 
            if S[j] != a[i][j] and S[j] != '?':  
                G[j] = S[j] 
        temp.append(G) 
        G = ['?'] * num_attributes 
        print(f"For Training Example No : {i+1} the hypothesis is S{i+1}", S) 
        print(f"For Training Example No : {i+1} the hypothesis is G{i+1}", temp)
