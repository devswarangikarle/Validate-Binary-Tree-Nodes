# Validate-Binary-Tree-Nodes
You have n binary tree nodes numbered from 0 to n - 1 where node i has two children leftChild[i] and rightChild[i], return true if and only if all the given nodes form exactly one valid binary tree.  If node i has no left child then leftChild[i] will equal -1, similarly for the right child. 

from collections import defaultdict
class Solution:
    def validateBinaryTreeNodes(self, n: int, leftChild: List[int], rightChild: List[int]) -> bool:
        graph = defaultdict(list)
        temp = {}
        for i in range(n):
            temp[i] = 1

        for i in range(n):
            if(leftChild[i]!=-1):
                graph[i].append(leftChild[i])
                if(leftChild[i] in temp):
                    del temp[leftChild[i]]
            if(rightChild[i]!=-1):
                graph[i].append(rightChild[i])
                if(rightChild[i] in temp):
                    del temp[rightChild[i]]

        if(len(temp)!=1):
            return False

        for key in temp.keys():
            root = key

        def dfs(node):
            if(node in visited):
                return False
            ans = True
            visited[node] = 1
            for child in graph[node]:
                ans = ans and dfs(child)
            return ans

        visited = {}
        ans = dfs(root)
        if(ans and len(visited)==n):
            return True
        return False
