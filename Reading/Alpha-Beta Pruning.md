[Minimax算法](https://en.wikipedia.org/wiki/Minimax)
- minimax algorithm, [极大极小算法](https://www.zhihu.com/question/27221568)</br>
  井字棋，英文名叫Tic-Tac-Toe; 井字策略，英文名叫Tic Tactics </br>
  我们可以看到，加上剪枝算法，我们不仅得到了相同的结果，而且减少了计算量。在实际应用中，加上剪枝算法，计算机大约需要算2*n^(x/2)个结果，如果n为分支数，x为步数。</br>
  相比于之前仅用极小极大算法的n^x，效率提高了很多。这也就意味着，如果在象棋比赛中，假设使用极小极大的算法，计算机能往前评估7步，加上剪枝算法，计算机能往前评估14步。极小极大和剪枝算法曾在IBM开发的国际象棋超级电脑，深蓝（Deep Blue）中被应用，并且两次打败当时的世界国际象棋冠军。</br>
  可参考 AIAM（Artificial Intelligence - A Modern Approach 人工智能：一种现代实现）的第五章</br>
Minimax (sometimes MinMax or MM[1]) is a decision rule used in decision theory, game theory, statistics and philosophy for minimizing the possible loss for a worst case (maximum loss) scenario. When dealing with gains, it is referred to as "maximin"—to maximize the minimum gain. Originally formulated for two-player zero-sum game theory, covering both the cases where players take alternate moves and those where they make simultaneous moves, it has also been extended to more complex games and to general decision-making in the presence of uncertainty.</br>
Minimax是一种决策规则，用于决策论、游戏论、统计、哲学， 用来最大限度的减少最坏情况下可能发生的损失。</br>
当处理增益，它被称为“最大最小”——最大化最小增益。最初是为两人零和游戏理论而设计的，它既包括双方采取交替动作的场合，也包括他们同时移动的情况，它也被扩展到更复杂的游戏中，并在不确定性的情况下进行一般决策。</br>
**In general games**</br>
The maximin value of a player is the highest value that the player can be sure to get without knowing the actions of the other players; equivalently, it is the lowest value the other players can force the player to receive when they know the player's action. Its formal definition is:[2]</br>
[](https://wikimedia.org/api/rest_v1/media/math/render/svg/76d2fe8fe2fc328093c7b0c19e83a0197004a5d3)</br>
一个球员的最大最小值，玩家一定要在不知道其他玩家的行为的最高价值；同样，这是其他球员可以迫使球员接受当他们知道玩家的行动值最低。
Where:

    i is the index of the player of interest. i是相应玩家编号；
    − i {\displaystyle -i} -i denotes all other players except player i. -i是除了i的其他所有玩家；
    a i {\displaystyle a_{i}} a_{i} is the action taken by player i. 玩家i采取的行动；
    a − i {\displaystyle a_{-i}} a_{{-i}} denotes the actions taken by all other players.除了玩家i的其他玩家采取的行动；
    v i {\displaystyle v_{i}} v_{i} is the value function of player i. 玩家i的价值公式；

Calculating the maximin value of a player is done in a worst-case approach: for each possible action of the player, we check all possible actions of the other players and determine the worst possible combination of actions—the one that gives player i the smallest value. Then, we determine which action player i can take in order to make sure that this smallest value is the highest possible.</br>
**计算玩家的极大极小值是在最坏的情况下做的：对于玩家每个可能的行动，我们检查其他玩家所有可能的行动来确定导致玩家i的最小价值的行动组合。然后，我们决定玩家i采取哪种动作，以确保这个最小值是最高的。**（*Q:为什么要这么做呢？ A:因为是零和游戏，此消彼长*）</br>

----
----

[Alpha-Beta Pruning wikipedia](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning)
- Alpha–beta pruning is a search algorithm that seeks to decrease the number of nodes that are evaluated by the minimax algorithm in its search tree. </br>
AlphaBeta剪枝算法是一个搜索算法旨在减少在其搜索树中，被极大极小算法评估的节点数。
- It is an adversarial search algorithm used commonly for machine playing of two-player games (Tic-tac-toe, Chess, Go, etc.). It stops completely evaluating a move when at least one possibility has been found that proves the move to be worse than a previously examined move. Such moves need not be evaluated further. When applied to a standard minimax tree, it returns the same move as minimax would, but prunes away branches that cannot possibly influence the final decision.[1]</br>
这是一个常用人机游戏对抗(井字棋，象棋，围棋等)的搜索算法。它的基本思想是根据上一层已经得到的当前最优结果，决定目前的搜索是否要继续下去。 </br>


