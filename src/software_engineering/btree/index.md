# Btree

What is a Btree? A Btree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time. The Btree generalizes the binary search tree, allowing for nodes with more than two children. Unlike self-balancing binary search trees, the Btree is optimized for systems that read and write large blocks of data, such as databases.

## Building a basic B-Tree

Steps:
1. Define a node structure.
2. Implement insertion and search functionality.
3. Handle splitting when a node overflows.

```go
package main

import (
	"fmt"
)

// BTreeNode represents a node in the B-Tree.
type BTreeNode struct {
	isLeaf   bool
	keys     []int
	children []*BTreeNode
}

// BTree represents the B-Tree structure.
type BTree struct {
	root  *BTreeNode
	order int // Max children per node
}

// NewBTree creates a new B-Tree with the given order.
func NewBTree(order int) *BTree {
	if order < 3 {
		panic("Order must be at least 3")
	}
	return &BTree{
		root: &BTreeNode{
			isLeaf: true,
			keys:   []int{},
		},
		order: order,
	}
}

// Search finds a key in the B-Tree.
func (t *BTree) Search(key int) *BTreeNode {
	return t.search(t.root, key)
}

func (t *BTree) search(node *BTreeNode, key int) *BTreeNode {
	i := 0
	// Find the position of the key or the child to follow.
	for i < len(node.keys) && key > node.keys[i] {
		i++
	}

	// Check if the key matches.
	if i < len(node.keys) && key == node.keys[i] {
		return node
	}

	// If it's a leaf node, key isn't present.
	if node.isLeaf {
		return nil
	}

	// Search in the child node.
	return t.search(node.children[i], key)
}

// Insert adds a key to the B-Tree.
func (t *BTree) Insert(key int) {
	root := t.root
	if len(root.keys) == t.order-1 {
		// Root is full; split it.
		newRoot := &BTreeNode{
			isLeaf:   false,
			children: []*BTreeNode{root},
		}
		t.splitChild(newRoot, 0)
		t.root = newRoot
	}
	t.insertNonFull(t.root, key)
}

func (t *BTree) insertNonFull(node *BTreeNode, key int) {
	i := len(node.keys) - 1

	if node.isLeaf {
		// Insert in the correct position in the leaf node.
		node.keys = append(node.keys, 0)
		for i >= 0 && key < node.keys[i] {
			node.keys[i+1] = node.keys[i]
			i--
		}
		node.keys[i+1] = key
	} else {
		// Find the child to insert into.
		for i >= 0 && key < node.keys[i] {
			i--
		}
		i++
		// Split the child if it's full.
		if len(node.children[i].keys) == t.order-1 {
			t.splitChild(node, i)
			if key > node.keys[i] {
				i++
			}
		}
		t.insertNonFull(node.children[i], key)
	}
}

func (t *BTree) splitChild(parent *BTreeNode, index int) {
	order := t.order
	child := parent.children[index]
	mid := order / 2

	// Create a new node for the split.
	newChild := &BTreeNode{
		isLeaf:   child.isLeaf,
		keys:     append([]int{}, child.keys[mid+1:]...),
		children: append([]*BTreeNode{}, child.children[mid+1:]...),
	}

	// Update the parent.
	parent.keys = append(parent.keys[:index], append([]int{child.keys[mid]}, parent.keys[index:]...)...)
	parent.children = append(parent.children[:index+1], append([]*BTreeNode{newChild}, parent.children[index+1:]...)...)

	// Trim the original child.
	child.keys = child.keys[:mid]
	child.children = child.children[:mid+1]
}

// PrintTree recursively prints the B-Tree.
func (t *BTree) PrintTree(node *BTreeNode, level int) {
	if node == nil {
		return
	}

	fmt.Printf("Level %d: %v\n", level, node.keys)
	for _, child := range node.children {
		t.PrintTree(child, level+1)
	}
}

func main() {
	// Create a new B-Tree with order 3.
	tree := NewBTree(3)

	// Insert some keys.
	keys := []int{10, 20, 5, 6, 12, 30, 7, 17}
	for _, key := range keys {
		tree.Insert(key)
	}

	// Print the tree structure.
	tree.PrintTree(tree.root, 0)

	// Search for a key.
	if node := tree.Search(12); node != nil {
		fmt.Println("Found key in node:", node.keys)
	} else {
		fmt.Println("Key not found")
	}
}

```