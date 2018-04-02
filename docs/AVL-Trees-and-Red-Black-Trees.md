AVL Trees are *self-balancing BSTs*

AVL Tree considered height balanced if the absolute value of the balance factor for each node is $\\leq$ 1

`BalanceFactor = heightOfRightSubtree - heightOfLeftSubtree`

**Insertion**

1. If subNode is NULL, return
2. If key is greater than the curr key, go right child.
3. If key is less than curr key, go left child.
3. Rebalance and update height (can be done inside rebalance)

**Removal**

1. find(SubNodeKey)
    + If find does not return a valid node, end the remove method.
2. Deal with children of node
    + If no children: just delete the node
    + Else if one child: overwrite removal node with its child
    + Else, there are two children:
	    - Find In Order Predecessor (IOP), which is the rightmost node in the left subtree.
	    - swap(IOP, root)
	    - remove(root->left)


**Rotations**

All rotations run in O(1) time, and are done in `rebalance()`. No rotations possible in `find()` call.

```cpp
void rotateRight(AVL*& root) {
	AVL* origRoot = root;
	root = root->left_;
	origRoot->left_ = root->right_;
	root->right_ = origRoot;

	updateHeight(root->right_);
	updateHeight(root);
}

void rotateLeft(AVL*& root) {
	AVL* origRoot = root;
	root = root->right_;
	origRoot->right_ = root->left_;
	root->left_ = origRoot;

	updateHeight(root->left_);
	updateHeight(root);
}

void rotateRightLeft(AVL*& root) {
	rotateRight(root->right_);
	rotateLeft(root);
}

void rotateLeftRight(AVL*& root) {
	rotateLeft(root->left_);
	rotateRight(root);
}

void rebalance(Node *&subtree) {
  int balance = getBalanceFactor(subtree);
  int leftBalance = getBalanceFactor(subtree->left);
  int rightBalance = getBalanceFactor(subtree->right);

  //If balance is negative, left heavy
  if (balance == - 2) {
    if (leftBalance == - 1) {
      rotateRight(subtree);
    } else rotateLeftRight(subtree);
  }
  //If balance is positive, right heavy
  if (balance == 2) {
    if (rightBalance) == 1) {
      rotateLeft(subtree);
    } else rotateRightLeft(subtree);
  }

  if (subtree != NULL) {
  	updateHeight(subtree);
  }
}
```

**Run Time Analysis**

|     AVL Operation     |  Run Time     |
|       ----       |     ----     |
|   find()         |  O(h) ** h = O(lg(n))  |
|   insert()       |  O(h) ** h = O(lg(n)) |
|   remove()       |  O(h) ** h = O(lg(n)) |
|   traverse()     |  O(n) |

**Summary of Advantages/Disadvantages for AVL Trees**

1. Advantages
	+ Run time of O(log(n)) is improvement over arrays and lists
	+ Great for specific implementations where exact key is unknown (Nearest neighbor, Interval search, etc.)
2. Disadvantages
	+ Not the fastest `find()` run time. Outperformed by hash tables.
	+ AVL tree does not work well with disk seeks. Must be stored in memory, so not good for large data sets.

## Red-Black Trees

When you see "Red-Black Tree", just think of an AVL Tree. They're both balanced BSTs.
