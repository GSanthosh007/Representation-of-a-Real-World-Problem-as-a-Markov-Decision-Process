# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim

To identify the task of a robot vacuum cleaner as a real-world sequential decision-making problem, and to represent it formally as a Markov Decision Process by defining its states, actions, rewards, transitions, and Python representation.

---

## Problem Statement

### Problem Description

A robot vacuum cleaner operates in a room and must decide, at each time step, what action to take based on the condition of the room and its own battery level. The outcome of each action is not always certain — for example, cleaning may or may not fully clean a dirty spot, and the battery may drain unpredictably. The robot must choose actions that keep the room clean while managing its battery efficiently. This makes it a good example of an MDP, since decisions must be made in sequence and each action affects future states.


---

## MDP Components

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space

The state space represents all possible conditions the robot vacuum cleaner can be in, based on the cleanliness of the room and its battery status.

```text
S = {
    Clean,
    Dirty,
    Low Battery,
    Charging
}
```



---

## Sample State

s = Dirty

This represents a situation where the robot detects that the room currently has dirt or debris and requires cleaning.

---

## Action Space

This means:

> Probability of reaching next state $s'$ after taking action $a$ in current state $s$.

P(Clean | Dirty, Clean) = 0.8
P(Dirty | Dirty, Clean) = 0.2

P(Clean | Clean, Move) = 0.7
P(Dirty | Clean, Move) = 0.3

P(Charging | Low Battery, Charge) = 1.0

P(Clean | Charging, Charge) = 1.0

---

## Reward Function

The reward function R(s,a,s') defines the feedback the robot receives after performing an action and reaching a new state.

General form:

$$
R(s,a,s')
$$

R(Dirty, Clean, Clean) = +5     → Room successfully cleaned

R(Dirty, Clean, Dirty) = -2     → Cleaning failed, room still dirty

R(Clean, Move, Clean)  = +1     → Efficient movement, room stays clean

R(Low Battery, Charge, Charging) = -1   → Battery too low, needs charging

R(Charging, Charge, Clean) = 0  → Neutral, robot recharges before resuming



---

## Graphical Representation

<img width="902" height="442" alt="image" src="https://github.com/user-attachments/assets/943e9289-b4ef-4c73-94c5-ee553b841034" />

---

## Python Representation
```
# ---- States ----
states = ["Clean", "Dirty", "Low Battery", "Charging"]

# ---- Actions ----
actions = ["Clean", "Move", "Charge"]

# ---- Transition Probabilities: P[state][action] = {next_state: probability} ----
P = {
    "Dirty": {
        "Clean": {"Clean": 0.8, "Dirty": 0.2}
    },
    "Clean": {
        "Move": {"Clean": 0.7, "Dirty": 0.3}
    },
    "Low Battery": {
        "Charge": {"Charging": 1.0}
    },
    "Charging": {
        "Charge": {"Clean": 1.0}
    }
}

# ---- Rewards: R[state][action] = reward value ----
R = {
    "Dirty": {"Clean": 5},
    "Clean": {"Move": 1},
    "Low Battery": {"Charge": -1},
    "Charging": {"Charge": 0}
}

# ---- Display the MDP ----
print("States:", states)
print("Actions:", actions)

print("\nTransition Probabilities:")
for s in P:
    for a in P[s]:
        print(f"  P(s'|{s},{a}) = {P[s][a]}")

print("\nRewards:")
for s in R:
    for a in R[s]:
        print(f"  R({s},{a}) = {R[s][a]}")
```



```python
# MDP Representation using Python
# print("Name: Santhosh G")
# print("Register Number:212223240152")

```

## Output

<img width="677" height="342" alt="image" src="https://github.com/user-attachments/assets/6132ef12-fdfa-4120-9a8d-2284b99714d4" />

## Result

The Markov Decision Process for the robot vacuum cleaner was successfully modeled with 4 states, 3 actions, transition probabilities, and rewards, and implemented using Python dictionaries. The formulation demonstrates how the robot can make sequential decisions to keep the room clean while managing its battery efficiently.

---



