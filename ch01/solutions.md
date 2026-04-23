# Exercise 1.1: Self-Play

Sure, let's focus on the aspects relevant to the question without mentioning symmetry.

In the case where the reinforcement learning algorithm plays against itself in tic-tac-toe:

1. **Exploration and Exploitation:** The algorithm will continue to explore different actions during its learning process. In self-play, it plays against an opponent that is also exploring different actions. Over time, both sides will learn from their experiences.

2. **Convergence to Optimal Strategy:** Given the deterministic nature of tic-tac-toe and the finite state space, the algorithm will eventually explore all possible states. As it continues to learn, it should converge to the optimal strategy for the game. The optimal strategy in tic-tac-toe is well-defined — either to win or to force a draw, depending on whether the player moves first or second.

Therefore, in this scenario, the reinforcement learning algorithm would likely learn the optimal policy for tic-tac-toe when playing against itself. The strategy learned should be one that maximizes the chances of winning or forcing a draw.

# Exercise 1.2: Symmetries

**Taking Advantage of Symmetries:**

1. **State Representation:** One way to amend the learning process is to use a more compact state representation that takes symmetries into account. Instead of treating symmetrically equivalent positions separately, the algorithm could represent them as the same state. For example, if a certain board configuration is a rotation or reflection of another, they can be treated as equivalent states.

2. **Value Sharing:** When updating the value estimates during the learning process, the algorithm can share the learned values between symmetrically equivalent states. If one state has been evaluated and found to be favorable, the same evaluation can be applied to its symmetrically equivalent counterparts.

**Improvements to the Learning Process:**

1. **Efficiency:** By exploiting symmetries, the learning process becomes more efficient. The algorithm needs to explore and learn from fewer distinct states, reducing the overall computational requirements.

2. **Generalization:** Learning from symmetrical positions allows the algorithm to generalize its knowledge across equivalent states. This can lead to a more robust and generalized understanding of the game, as it is learning from a more diverse set of experiences.

**Considering the Opponent's Strategy:**

If the opponent does not take advantage of symmetries, it might still be beneficial for the learning algorithm to do so. By exploiting symmetries, the algorithm gains efficiency and generalization benefits. However, the exact impact depends on the opponent's strategy and the extent to which symmetries are present in the game.

**Symmetrically Equivalent Positions and Values:**

It is not necessarily true that symmetrically equivalent positions should have the same value. While symmetrical positions may share similar values due to the nature of the game, there could be cases where the optimal move differs between symmetrically equivalent positions. The algorithm should learn to distinguish between such subtleties and assign appropriate values based on the specific context of the game.

# Exercise 1.3: Greedy Play

**Learning Better or Worse:**

1. **Possibility of Learning Better:** A greedy strategy might lead the player to consistently choose moves that, based on its current knowledge, are perceived as the best in terms of immediate reward or value. If the learning algorithm has converged to an accurate evaluation function, the greedy player could potentially make optimal moves in each situation, leading to better overall performance.

2. **Risk of Learning Worse:** However, there's a risk that a purely greedy strategy may not explore enough during the learning process. Exploration is crucial for discovering new, potentially better strategies. If the learning algorithm hasn't explored a diverse set of moves, it might miss out on discovering superior long-term strategies, leading to suboptimal play.

**Problems with Greedy Play:**

1. **Lack of Exploration:** Greedy play can lead to a lack of exploration, preventing the algorithm from discovering alternative, potentially better moves. This lack of exploration is particularly problematic when the learning algorithm hasn't fully converged to an accurate evaluation function.

2. **Local Optima:** The player might get stuck in local optima, settling for what seems like the best move based on its current knowledge but missing out on globally better strategies. This can hinder the learning process, especially if there are complex interactions and dependencies between moves.

3. **Failure to Adapt:** A purely greedy player might struggle to adapt to changes in the opponent's strategy or to unforeseen circumstances. Learning a more flexible and adaptive policy often requires exploration and a willingness to deviate from the immediate best-rated move.

In summary, a reinforcement learning player that always plays the move it rates as the best (a greedy player) might learn to play well if it has accurately converged to the optimal strategy. However, there is a risk of getting stuck in suboptimal strategies due to the lack of exploration. Striking a balance between exploitation and exploration is crucial for effective learning and adaptive play.

# Exercise 1.4: Learning from Exploration

1. **Learning from Exploratory Moves:**
   - **Concept:** When learning from exploratory moves, the learning algorithm updates its state values even when it takes exploratory actions. Exploratory moves are those that deviate from the current best-known policy to encourage exploration and the discovery of potentially better strategies.
   - **Effect:** This approach allows the algorithm to refine its understanding of the value of states, including those visited during exploration. Over time, it converges to a set of probabilities that takes into account both exploitative and exploratory aspects.

2. **Not Learning from Exploratory Moves:**
   - **Concept:** If learning updates occur only for exploitative moves (non-exploratory moves), the algorithm would update its state values based solely on the moves it considers to be the best at each point in time.
   - **Effect:** This approach might lead to a more myopic view, as the algorithm would not update its values based on the information gained from exploratory actions. It could potentially converge to a set of probabilities that are less adaptive to changes in the environment or opponent's strategy.

**Which Set of Probabilities Might be Better to Learn?**

The set of probabilities learned from exploratory moves is conceptually better for a few reasons:

1. **Adaptability:** Learning from exploratory moves allows the algorithm to adapt and adjust its strategies based on new information gained through exploration. This adaptability is crucial for dealing with changes in the environment or opponent's behavior.

2. **Robustness:** The set of probabilities learned from exploration is likely to be more robust as it considers a broader range of actions and scenarios. It is less prone to getting stuck in local optima and can discover superior strategies through exploration.

**Resulting in More Wins:**

Learning from exploratory moves is more likely to result in more wins. By exploring alternative actions and updating values based on those explorations, the algorithm is better equipped to discover optimal strategies. It can learn from both successful and unsuccessful exploratory moves, refining its policy over time to increase the chances of winning.

# Exercise 1.5: Other Improvements

**Other Ways to Improve the Reinforcement Learning Player:**

1. **Function Approximation:** Instead of tabular methods, which may be impractical for large state spaces, using function approximation techniques like linear function approximation or neural networks can be considered. This allows the player to generalize its learning to unseen states.

2. **Experience Replay:** Implementing experience replay, where past experiences are stored and randomly sampled during learning, can lead to more stable and efficient learning. This technique is often used in combination with function approximation methods.

3. **Learning from Human Experts:** Incorporating knowledge from human experts or pre-existing strategies can bootstrap the learning process. The algorithm can start with some prior knowledge and refine it through reinforcement learning.

4. **Monte Carlo Tree Search (MCTS):** MCTS is a tree-based search algorithm that combines tree exploration and exploitation. It has been successful in various board games and might be adapted to improve the tic-tac-toe player.

5. **Dynamic Learning Rates:** Using adaptive learning rates that change based on the observed dynamics of the environment can enhance the learning process. Techniques like the Adagrad or Adam optimizers can be explored.

**Better Ways to Solve the Tic-Tac-Toe Problem:**

1. **Optimal Policy Pre-computation:** Since tic-tac-toe has a small state space, it's possible to precompute the optimal policy for every possible state. This eliminates the need for learning during gameplay. However, it assumes perfect knowledge of the environment.

2. **Game-Specific Heuristics:** Incorporating domain-specific heuristics based on known optimal strategies in tic-tac-toe can guide the learning process. These heuristics can provide a strong initial policy to build upon.

3. **Pattern Recognition:** Utilizing pattern recognition techniques to identify recurring board patterns associated with winning or losing can enhance the learning process. The algorithm can then use this knowledge to make more informed decisions.

4. **Ensemble Methods:** Combining multiple reinforcement learning models or strategies using ensemble methods can lead to a more robust and reliable tic-tac-toe player.

It's important to note that the choice of improvement strategies depends on the specific characteristics of the problem and the desired trade-offs between computational complexity and performance. Experimentation and tuning are often necessary to determine the most effective approach.