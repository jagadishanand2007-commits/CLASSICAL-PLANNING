# ExpNo:10 Implementation of Classical Planning Algorithm
<h3>Name: Jagadish Janardhanan A
<h3>Register Number: 212224060102
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
# Program:
    # ----------------- CLASSICAL PLANNING -----------------
    from collections import deque

    def states_match(state1, state2):
    """Check if all key-value pairs in state2 match state1"""
    for key, val in state2.items():
        if state1.get(key) != val:
            return False
    return True

    def apply_action(state, action_effect):
    """Return a new state after applying the action"""
    new_state = state.copy()
    new_state.update(action_effect)
    return new_state

    def find_plan(initial_state, goal_state, actions):
    """Find a sequence of actions to reach the goal using BFS"""
    frontier = deque()
    frontier.append((initial_state, []))
    visited = []

    while frontier:
        current_state, plan = frontier.popleft()
        if states_match(current_state, goal_state):
            return plan
        visited.append(current_state)

        for action_name, action_info in actions.items():
            precond = action_info['precondition']
            effect = action_info['effect']

            if states_match(current_state, precond):
                new_state = apply_action(current_state, effect)
                if new_state not in visited:
                    frontier.append((new_state, plan + [action_name]))
    return None

    # ----------------- EXAMPLE -----------------
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
    print("Plan to reach goal:", plan)

# Output:
<img width="957" height="373" alt="image" src="https://github.com/user-attachments/assets/c3c19c11-1b48-41bb-b4ae-bcc15a77a7df" />

# Result:
find_plan(initial_state, goal_state, actions) searches the state space using a strategy like BFS to generate a sequence of actions whose preconditions are satisfied and effects lead from the initial state to the goal state. It returns the plan as a list of actions or None if no plan exists.
  

