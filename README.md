# AI-versus-Nim
Playing Nim Game against AI


### Objective
Create an AI that teaches itself to play the game of Nim using reinforcement learning with the ε-Greedy Q-Learning method.

### Game Overview
Nim is a two-player game where players take turns removing objects from several piles. Each turn, a player must remove at least one object from a single pile. The objective is to force the opponent to take the last object. Our implementation plays in "misère" format, meaning the player who removes the last object loses.

### Solution Strategy
The game of Nim has a known mathematical solution involving the "nim-sum" (XOR of all pile sizes), which can guide an optimal strategy. However, this project trains an AI to discover its own strategy through **reinforcement learning**, without prior knowledge of nim-sum.

### Reinforcement Learning with Q-Learning
In Q-Learning, an AI agent learns the values of actions in different states by observing rewards or penalties and updating its knowledge with each move. Key concepts:

1. **Q-Value**: Q(s, a) estimates the reward for taking action `a` in state `s`.
2. **Learning Process**: The AI begins with no knowledge (Q-values set to 0). With each game, it updates Q-values based on rewards, adjusting its future choices.
3. **Q-Value Update Formula**:
   \[
   Q(s, a) \leftarrow \text{old value} + \alpha \times (\text{reward} + \text{future reward} - \text{old value})
   \]
   where `α` (learning rate) determines how much the agent values new vs. old information.

### ε-Greedy Decision Making
A purely greedy strategy (always taking the highest Q-value action) risks missing optimal moves. In ε-Greedy strategy:
- The AI explores random actions with probability `ε` (to discover new strategies).
- With probability `1-ε`, it picks the action with the highest Q-value.
  
This balance allows the AI to learn the best moves while also exploring new ones.

### Implementation Details
1. **State Representation**: The game state is a list of pile sizes, e.g., `[1, 1, 3, 5]`.
2. **Action Representation**: Actions are pairs `(i, j)`, where `i` is the pile index and `j` is the number of objects to remove from that pile.

### Functions to Implement
1. **get_q_value(state, action)**: Returns the Q-value for a given state-action pair from the `self.q` dictionary (or 0 if it’s unknown).
2. **update_q_value(state, action, old_q, reward, future_rewards)**: Updates the Q-value for a state-action pair based on the Q-learning formula.
3. **best_future_reward(state)**: Returns the highest Q-value for any action in a given state.
4. **choose_action(state, epsilon)**: Selects an action based on ε-Greedy strategy. If `epsilon` is `False`, it picks the best action; otherwise, it uses the ε-Greedy approach.

### Usage
Run with Python to train and play the AI over multiple games (default is 10,000):

```bash
python play.py [num_games=10000]
