---
layout: post
title: "Morris traversal"
date: 2017-08-10
permalink: /technique/:year/:month/:day/:title
section: "technique"
---

### What is Morris Traversal
It solves the problem of traverse binary tree with O(1) space and without affecting tree's structure.

最大的难点在于，遍历到子节点的时候怎样重新返回到父节点（假设节点中没有指向父节点的p指针）==> 利用叶子节点中的左右空指针指向某种顺序遍历下的前驱节点或后继节点。

### In order traversal
1. 如果当前节点的左孩子为空，则输出当前节点并将其右孩子作为当前节点。

2. 如果当前节点的左孩子不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点。

   a) 如果前驱节点的右孩子为空，将它的右孩子设置为当前节点。当前节点更新为当前节点的左孩子。

   b) 如果前驱节点的右孩子为当前节点，将它的右孩子重新设为空（恢复树的形状）。输出当前节点。当前节点更新为当前节点的右孩子。

3. 重复以上1、2直到当前节点为空。

```java
    public class Solution {
        public List<Integer> InOrder(TreeNode root) {
            TreeNode curr = root;
            List<Integer> result = new ArrayList<Integer>();
            while(curr != null) {
                if(curr.left == null) {
                    result.add(curr.val);
                    curr = curr.right;
                } else {
                    TreeNode prev = findRightMost(curr.left);
                    if(prev.right == curr) {
                        prev.right == null;
                        result.add(curr.val);
                        curr = curr.right;
                    } else {
                        prev.right = curr;
                        curr = curr.left;
                    }
                }
            }
            return result;
        }

        private TreeNode findRightMost(TreeNode root) {
            while(root.right != null) {
                root = root.right;
            }
            return root;
        }
    }
```

> Exercise: recover binary search tree
```java
    public class Solution {
        public void recoverTree(TreeNode root) {
            TreeNode[] pair = new TreeNode[2];
            TreeNode prev = null;
            TreeNode curr = root;
            
            while(curr != null) {
                if(curr.left == null) {
                    // process curr
                    if(prev != null) {
                        if(prev.val > curr.val) {
                            if(pair[0] == null) {
                                pair[0] = prev;
                            }
                            pair[1] = curr;
                        }
                    }
                    
                    prev = curr;
                    curr = curr.right;
                } else {
                    TreeNode tmp = findPrev(curr);
                    if(tmp.right == null) {
                        tmp.right = curr;
                        curr = curr.left;
                    } else {
                        tmp.right = null;
                        
                        // process curr
                        if(prev != null) {
                            if(prev.val > curr.val) {
                                if(pair[0] == null) {
                                    pair[0] = prev;
                                }
                                pair[1] = curr;
                            }
                        }
                        
                        prev = curr;
                        curr = curr.right;
                    }
                }
            }
            
            // swap
            int val = pair[0].val;
            pair[0].val = pair[1].val;
            pair[1].val = val;
        }
        
        private TreeNode findPrev(TreeNode root) {
            TreeNode curr = root.left;
            // because Morris add link, this will have infinite loop
            while(curr.right != null && curr.right != root) {
                curr = curr.right;
            }
            return curr;
        }
    }
```

### Pre order traversal
1. 如果当前节点的左孩子为空，则输出当前节点并将其右孩子作为当前节点。

2. 如果当前节点的左孩子不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点。

   a) 如果前驱节点的右孩子为空，将它的右孩子设置为当前节点。输出当前节点（在这里输出，这是与中序遍历唯一一点不同）。当前节点更新为当前节点的左孩子。

   b) 如果前驱节点的右孩子为当前节点，将它的右孩子重新设为空。当前节点更新为当前节点的右孩子。

3. 重复以上1、2直到当前节点为空。

```java
    public class Solution {
        public List<Integer> InOrder(TreeNode root) {
            TreeNode curr = root;
            List<Integer> result = new ArrayList<Integer>();
            while(curr != null) {
                if(curr.left == null) {
                    result.add(curr.val);
                    curr = curr.right;
                } else {
                    TreeNode prev = findRightMost(curr.left);
                    if(prev.right == curr) {
                        prev.right == null;
                        curr = curr.right;
                    } else {
                        result.add(curr.val);
                        prev.right = curr;
                        curr = curr.left;
                    }
                }
            }
            return result;
        }

        private TreeNode findRightMost(TreeNode root) {
            while(root.right != null) {
                root = root.right;
            }
            return root;
        }
    }

```

### Post order traversal
_(:з」∠)_

### Reference
1. [Morris Traversal方法遍历二叉树](http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)