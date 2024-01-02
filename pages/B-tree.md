tags:: [[DSA]], [[Data Structure]]

- # B-tree
	- A B-tree is a specialized data structure used for organizing and storing data in a sorted manner to allow for efficient insertion, deletion, and searching operations. It's particularly useful in scenarios where large amounts of data need to be stored and accessed quickly, commonly used in databases and file systems.
	- ## Characteristics of a B-tree
		- **Balanced Tree**
			- A B-tree is a self-balancing tree, meaning it maintains a balanced structure regardless of the order and frequency of insertions and deletions. This balance is crucial for ensuring consistent search and retrieval times.
		- **Node Structure**
			- Nodes in a B-tree can have multiple keys and child pointers. Unlike binary trees, which have two child nodes per parent, B-trees can have a varying number of children, typically ranging from a specific minimum to a maximum number defined by the order of the tree.
		- **Ordered Data**
			- Data within a B-tree is stored in a sorted order. Each node maintains keys in ascending (or descending) order, facilitating efficient searching using algorithms like binary search.
	- ## Structure of a B-tree
		- **Root Node**
			- The topmost node of the B-tree. Initially, it may contain a small number of keys and pointers.
		- **Internal Nodes**
			- Intermediate nodes between the root and the leaf nodes. These nodes contain a range of keys used to guide the search down the tree.
		- **Leaf Nodes**
			- The bottommost nodes of the tree. They contain actual data entries or pointers to the actual data. In some variations of B-trees, leaf nodes might also contain keys with associated data.
	- ## Operations in a B-tree
		- **Insertion**
			- When inserting a new element into a B-tree, the tree ensures that the insertion maintains its balance. If a node becomes full after insertion, it may split, redistributing keys and promoting a median key to the parent node.
		- **Deletion**
			- Deleting an element requires rebalancing the tree to maintain its properties. It may involve merging nodes or redistributing keys among nodes.
		- **Search**
			- B-trees use a process similar to binary search to locate elements efficiently. Starting from the root, the search moves down the tree by comparing the search key with keys in the nodes until it reaches the appropriate leaf node.
	- ## Benefits of using a B-tree
		- **Efficiency**
			- B-trees offer logarithmic time complexity for search, insertion, and deletion operations, making them suitable for handling large datasets efficiently.
		- **Versatility**
			- They adapt well to different storage systems and access patterns, making them a favored structure in databases and file systems.
		- **Balanced Nature**
			- Their self-balancing property ensures consistent performance even with dynamic datasets.
	- B-trees are a fundamental part of many database systems due to their ability to efficiently store and retrieve large amounts of data while maintaining a balanced structure that optimizes search and modification operations.
	- ## Implementations of B-tree
		- ```go
		  package main
		  
		  import (
		  	"fmt"
		  )
		  
		  const t = 3
		  
		  type Node struct {
		  	leaf     bool
		  	n        int
		  	keys     []int
		  	children []*Node
		  }
		  
		  func NewNode(leaf bool) *Node {
		  	return &Node{
		  		leaf:     leaf,
		  		n:        0,
		  		keys:     make([]int, 2*t-1),
		  		children: make([]*Node, 2*t),
		  	}
		  }
		  
		  func (n *Node) Traverse() {
		  	fmt.Println("Keys:")
		  	for i := 0; i < n.n; i++ {
		  		fmt.Printf("%d ", n.keys[i])
		  	}
		  	fmt.Println()
		  
		  	if !n.leaf {
		  		fmt.Println("Children:")
		  		for i := 0; i < n.n+1; i++ {
		  			n.children[i].Traverse()
		  		}
		  	}
		  }
		  
		  func (n *Node) Search(k int) *Node {
		  	i := 0
		  	for i < n.n && k > n.keys[i] {
		  		i++
		  	}
		  
		  	if i < n.n && k == n.keys[i] {
		  		return n
		  	} else if n.leaf {
		  		return nil
		  	} else {
		  		return n.children[i].Search(k)
		  	}
		  }
		  
		  func (n *Node) InsertNonFull(k int) {
		  	i := n.n - 1
		  
		  	if n.leaf {
		  		for i >= 0 && k < n.keys[i] {
		  			n.keys[i+1] = n.keys[i]
		  			i--
		  		}
		  		n.keys[i+1] = k
		  		n.n++
		  	} else {
		  		for i >= 0 && k < n.keys[i] {
		  			i--
		  		}
		  
		  		i++
		  		if n.children[i].n == 2*t-1 {
		  			n.SplitChild(i, n.children[i])
		  
		  			if k > n.keys[i] {
		  				i++
		  			}
		  		}
		  		n.children[i].InsertNonFull(k)
		  	}
		  }
		  
		  func (n *Node) SplitChild(i int, y *Node) {
		  	z := NewNode(y.leaf)
		  	z.n = t - 1
		  
		  	for j := 0; j < t-1; j++ {
		  		z.keys[j] = y.keys[j+t]
		  	}
		  	if !y.leaf {
		  		for j := 0; j < t; j++ {
		  			z.children[j] = y.children[j+t]
		  		}
		  	}
		  
		  	y.n = t - 1
		  
		  	for j := n.n; j >= i+1; j-- {
		  		n.children[j+1] = n.children[j]
		  	}
		  	n.children[i+1] = z
		  
		  	for j := n.n - 1; j >= i; j-- {
		  		n.keys[j+1] = n.keys[j]
		  	}
		  	n.keys[i] = y.keys[t-1]
		  
		  	n.n++
		  }
		  
		  type BTree struct {
		  	root *Node
		  }
		  
		  func NewBTree() *BTree {
		  	return &BTree{
		  		root: NewNode(true),
		  	}
		  }
		  
		  func (b *BTree) Insert(k int) {
		  	root := b.root
		  	if root.n == 2*t-1 {
		  		s := NewNode(false)
		  		s.children[0] = root
		  		s.SplitChild(0, root)
		  
		  		i := 0
		  		if s.keys[0] < k {
		  			i++
		  		}
		  		s.children[i].InsertNonFull(k)
		  
		  		b.root = s
		  	} else {
		  		root.InsertNonFull(k)
		  	}
		  }
		  
		  func main() {
		  	btree := NewBTree()
		  
		  	keys := []int{3, 7, 2, 9, 1, 5, 8, 4, 6}
		  
		  	for _, key := range keys {
		  		btree.Insert(key)
		  	}
		  
		  	fmt.Println("B-tree traversal start\n")
		  	btree.root.Traverse()
		  
		  	searchKey := 5
		  	result := btree.root.Search(searchKey)
		  	if result != nil {
		  		fmt.Printf("Key %d found!\n", searchKey)
		  	} else {
		  		fmt.Printf("Key %d not found.\n", searchKey)
		  	}
		  	
		  	fmt.Println("\nB-tree traversal complete")
		  }
		  ```
			- ```shell
			  B-tree traversal start
			  
			  Keys:
			  3 7 
			  Children:
			  Keys:
			  1 2 
			  Keys:
			  4 5 6 
			  Keys:
			  8 9 
			  Key 5 found!
			  
			  B-tree traversal complete
			  ```
	- ## B-Tree Resources
		- [B-tree - Wikipedia](https://en.wikipedia.org/wiki/B-tree#:~:text=In%20computer%20science%2C%20a%20B,with%20more%20than%20two%20children.)