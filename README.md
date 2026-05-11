# ExpNo:10 Implementation of Classical Planning Algorithm

<h3>NAME: RAMADEVI V </h3>
<h3>RESITER NUMBER: 212224060208 </h3>

# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

<h3>PROGRAM: </h3>

```
from collections import deque
import copy

def is_goal(state, goal_state):
    for key in goal_state:
        if state.get(key) != goal_state[key]:
            return False
    return True


def applicable(state, action):
    """Check if action preconditions are satisfied"""
    for key in action['precondition']:
        if state.get(key) != action['precondition'][key]:
            return False
    return True


def apply_action(state, action):
    """Return new state after applying action"""
    new_state = copy.deepcopy(state)
    for key in action['effect']:
        new_state[key] = action['effect'][key]
    return new_state


def find_plan(initial_state, goal_state, actions):
    queue = deque()
    visited = set()

    queue.append((initial_state, []))
    visited.add(tuple(sorted(initial_state.items())))

    while queue:
        current_state, plan = queue.popleft()

        if is_goal(current_state, goal_state):
            return plan

        for action_name, action in actions.items():
            if applicable(current_state, action):
                new_state = apply_action(current_state, action)

                state_tuple = tuple(sorted(new_state.items()))
                if state_tuple not in visited:
                    visited.add(state_tuple)
                    queue.append((new_state, plan + [action_name]))

    return None

#example

initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {
        'precondition': {'A': 'Table', 'B': 'Table'},
        'effect': {'A': 'B'}
    },
    'move_B_to_Table': {
        'precondition': {'A': 'Table', 'B': 'B'},
        'effect': {'B': 'Table'}
    }
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)

initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {
        'precondition': {'A': 'Table', 'B': 'Table'},
        'effect': {'A': 'B'}
    },
    'move_B_to_C': {
        'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'},
        'effect': {'B': 'C'}
    },
    'move_C_to_Table': {
        'precondition': {'A': 'B', 'B': 'C', 'C': 'C'},
        'effect': {'C': 'Table'}
    }
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
<h3>OUTPUT: </h3>
<img width="872" height="231" alt="image" src="https://github.com/user-attachments/assets/a5af802c-b46d-4827-a8ea-b99bbbff8e8b" />
<h3>RESULT: </h3>
Therefore, Implementation of Classical Planning Algorithm is implemetated successfully.



