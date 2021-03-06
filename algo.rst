=============================
动态规划: dynamic programming
=============================

适用问题
---------
暴力穷举算法求最值问题。

- 重叠子结构: 重复计算某一个子问题。如果存在，则将结果储存起来以避免重复计算而实现优化。
- 最优子结构: 从子问题的最优解推导出更大规模问题的最优解，类似与链式反应。
- 状态转移方程


算法框架
---------

.. code-block:: C++

   # 初始化 base case
   dp[0][0][...] = base
   # 进行状态转移
   for 状态1 in 状态1的所有取值：
       for 状态2 in 状态2的所有取值：
           for ...
               dp[状态1][状态2][...] = 求最值(选择1，选择2...)

注意
------

#. 如何遍历状态?

   - 在遍历状态的过程中，一定要确保新的状态是基于已经算过的状态而产生的。
   - 不一定都是正向遍历。遍历状态的过程取决与base case到目标状态的方向。

#. 状态压缩优化空间复杂度

   如果状态转移方程中，新状态的产生总是只依赖于相邻几个状态，则可以进行状态压缩(DP table)。


--------------------------------

==============
回溯算法
==============

适用问题
---------
暴力穷举算法，解决一个回溯问题，本质上就是一个决策树的遍历过程。
从一副图中找到起点到终点的最短距离。


算法框架
---------

`N`叉树的遍历过程。

.. code-block:: C++

   result = []
   def backtrack(路径, 选择列表):
       if 满足结束条件:
           result.add(路径)
           return

       // `N`叉树的遍历
       for 选择 in 选择列表:
           做选择
           backtrack(路径, 选择列表)
           撤销选择

--------------------------------

==============
BFS 广度优先
==============

适用问题
---------
从一副图中找到起点到终点的最短距离。


算法框架
---------

.. code-block:: C++

   // 计算从起点 start 到终点 target 的最近距离
   int BFS(Node start, Node target) {
       Queue<Node> q; // 核心数据结构
       Set<Node> visited; // 避免走回头路

       q.offer(start); // 将起点加入队列
       visited.add(start);
       int step = 0; // 记录扩散的步数

       while (q not empty) {
           int sz = q.size();
           /* 将当前队列中的所有节点向四周扩散 */
           for (int i = 0; i < sz; i++) {
               Node cur = q.poll();
               /* 划重点：这里判断是否到达终点 */
               if (cur is target)
                   return step;
               /* 将 cur 的相邻节点加入队列 */
               for (Node x : cur.adj())
                   if (x not in visited) {
                       q.offer(x);
                       visited.add(x);
                   }
           }
           /* 划重点：更新步数在这里 */
           step++;
       }
   }
