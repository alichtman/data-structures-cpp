## Dictionaries

Can be implemented with: Binary Tree, BST, AVL, B-Tree

All keys must be unique

|     Methods     |   Data Struct     |   Data Struct    |
|      ----       |     ----         |    ----      |
| insert(K key, V val)  |  O(1)   |     Amortized O(1)     |
| remove(K key)   |  O(1)  | O(1)  |
| find(K key)     |  O(1)   |     Amortized O(1)     |


You can access elements in a map with the `[]` operator, just like arrays and vectors, but you have to be careful. If key doesn’t exist in the map, m[key] will create a default value for the key, insert it into m and then return a reference to it. Because of this, you can’t use `[]` on a const map.

For each `key_val` in `map`, do...
```cpp
map<int, string> map;
for (std::pair<const int, string> & key_val : map)
{
    cout << key_val.first << ", " << key_val.second << endl;
}
```

Memoization is an optimization technique that stores the result of expensive function calls and returns a cached result when the same inputs occur again.

## Hash Tables

Keyspace: Number of valid keys for a set of data

**Accessing Key Value Pairs**

1. Key: `kvPair->first`
2. Value: `kvPair->second`

**Hash Table**

Trade memory efficiency for run time efficiency.

Hash Tables replace BSTs and Linked Lists.

Needs three things:

1. Hash Function
2. Array : Constant Time Operations, Deterministic, SUHA
3. Collision Avoidance Strategy

**Shortcomings of Hash Tables**

1. Can't use hash tables for every problem because they are unordered and unstructured. Not possible to do a ranged search, or nearest neighbor search (BSTs can do these.)
2. Memory Overhead
3. Collisions

**Hash Functions**

+ A perfect hash function is a bijection: *One-to-One* and *Onto*

+ Characteristics of a Good Hash Function:
	- Constant Time: `O(1)`
	- Deterministic: No Randomness. If `k == j`, then `hash(k) == hash(j)`
	- SUHA

+ SUHA (Simple Uniform Hashing Assumption) -- Keys are uniformly distributed.
	- Each key has an equal probability of hashing to a particular index.
	- \\(Probability = \frac{1}{N}\\), where N is the size of the array
	- Hash of key doesn't depend on any previous insertions.

**Load Factor**

+ \\(loadFactor = \frac{filledArrayCells}{arraySize}\\)
+ As load factor increases, run time increases.
+ If load factor is held constant, run time is fixed.

**Hash Table Implementation**

1. Array with size of first *prime* number greater than keyspace.
2. Resize when load factor is above a certain threshold (`0.7`) by doubling the size and finding the next largest *prime* number.

**Run Times**

| Function    |  Run Time |
|     ----    |   ----    |
| insert()    |    O(1)   |
| find()      |    O(1)   |
| remove()    |    O(1)   |

**Collision Avoidance Strategies**

1. Linear Probing -- Open Addressing
	+ Only one hash function

	+ Insert
		- Check for resize
		- Key hashed to get an attempted insertion index
			- If space is free, insert at index.
			- If space is occupied, increment index until free space found.

	+ Find
		- Key is hashed to get start search index.
		- Check search index and increment until either hit search key OR hit NULL.

	+ Remove
		- Key hashed to get start search index.
		- Increment until search key found
		- Set that space to NULL and rehash everything after it until next NULL space.

	+ Issue: Linear Probing leads to Primary Clustering. Double Hashing solves this.

2. Double Hashing -- Open Addressing
	+ Two hash functions
		- First hash: insertion_index.
		- Second hash: step_value.

	+ Insert
		- Increment number of elements.
		- If we should resize, then resize the table.
		- Hash the original key using hash1 to get insertion index.
		- Hash the original key using hash2 to get the skip number.
		- While value at insertion index is filled
			- Update `insertion_index = (insertion_index + skip) % sizeOfTable`
		- `insertion_index` is now guaranteed to be valid. Insert there.

	+ Find
		- Hash original key w/ hash1, saving as the `insertion_index`.
		- Hash original key w/ hash2, saving as `skip_num`.
		- While value at an `insertion_index` is not `NULL`
			- If value of object at `insertion_index` is `search_key`, return it.
			- Else `insertion_index = (insertion_index + skip_num) % size`

	+ Remove
		- Key hashed by both functions to get search index and step
		- Increment by step until search key found
		- Set that space to NULL and rehash everything that is step spaces after it until NULL space.

	```cpp
	void remove(const K& key) {
	    unsigned insertion_index = hash(key);
	    unsigned skipNum = hash2(key);

	    while(table[insertion_index] != NULL && table[insertion_index]->first != key){
	        insertion_index = (insertion_index + skipNum) % (table.size() - 1);
	    }

	    if (table[insertion_index] == NULL) {
	        return;
	    }

	    //Remove searchKey
	    table[insertion_index] = NULL;
	    insertion_index = (insertion_index + skipNum) % (table.size() - 1);

	    //Cycle through all other keys that could have been misplaced due to a collision.
	    //Remove them and then insert them by rehashing
	    while (table[insertion_index] != NULL){
	        Pair<K,V> temp = table[insertion_index];
	        table[insertion_index] = NULL;
	        insert(temp->first, temp->second);
	        insertion_index = (insertion_index + skipNum) % (table.size() - 1);
	    }
	}
	```

3. Separate Chaining -- Use for Large Data Sets
	- Array of linked lists
	- Only one hash function

	+ Insert
		- Key hashed to get insertion index.
		- Insert the key at the beginning of the linked list for O(1) insert

	+ Find
		- Key hashed to get search index.
		- Iterate through linked list until hit key or hit NULL.

	+ Remove
		- Key hashed to get removal index.
		- Iterate through linked list until hit key or hit NULL
			- If NULL, elem doesn't exist.
			- Else, remove it from the linked list.

**Collision Avoidance Strategy Summary**

Use Separate Chaining for large data sets.

Use Linear Probing and Double Hashing for fast structure speed.