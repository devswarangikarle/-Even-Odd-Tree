# -Even-Odd-Tree
A binary tree is named Even-Odd if it meets the following conditions:  The root of the binary tree is at level index 0, its children are at level index 1, their children are at level index 2, etc. For every even-indexed level, all nodes at the level have odd integer values in strictly increasing order (from left to right). 

class Solution:
    def isEvenOddTree(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True

        queue = deque([root])
        level = 0

        while queue:
            prev_val = None  
            for _ in range(len(queue)):
                node = queue.popleft()

                if (level % 2 == 0 and (node.val % 2 == 0 or (prev_val is not None and node.val <= prev_val))) or \
                   (level % 2 == 1 and (node.val % 2 == 1 or (prev_val is not None and node.val >= prev_val))):
                    return False

                prev_val = node.val

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            level += 1

        return True
