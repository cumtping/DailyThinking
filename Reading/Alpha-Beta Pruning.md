[wikipedia](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning)
- Alpha–beta pruning is a search algorithm that seeks to decrease the number of nodes that are evaluated by the minimax algorithm in its search tree. 
AlphaBeta剪枝算法是一个搜索算法旨在减少在其搜索树中，被极大极小算法评估的节点数。
----
- minimax algorithm, [极大极小算法](https://www.zhihu.com/question/27221568)</br>
  井字棋，英文名叫Tic-Tac-Toe; 井字策略，英文名叫Tic Tactics </br>
  我们可以看到，加上剪枝算法，我们不仅得到了相同的结果，而且减少了计算量。在实际应用中，加上剪枝算法，计算机大约需要算2*n^(x/2)个结果，如果n为分支数，x为步数。
  相比于之前仅用极小极大算法的n^x，效率提高了很多。这也就意味着，如果在象棋比赛中，假设使用极小极大的算法，计算机能往前评估7步，加上剪枝算法，计算机能往前评估14步。
  极小极大和剪枝算法曾在IBM开发的国际象棋超级电脑，深蓝（Deep Blue）中被应用，并且两次打败当时的世界国际象棋冠军。
- 
----
