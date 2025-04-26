[DBDB](https://aosabook.org/en/500L/dbdb-dog-bed-database.html) (Dog Bed Database) is a Python library that implements a simple key/value database. It lets you associate a key with a value, and store that association on disk for later retrieval.

DBDB aims to preserve data in the face of computer crashes and error conditions. It also avoids holding all data in RAM at once so you can store more data than you have RAM.

---

**tool.py** defines a command-line tool for exploring a database from a terminal window.

**interface.py** defines a class (DBDB) which implements the Python dictionary API using the concrete BinaryTree implementation. This is how you'd use DBDB inside a Python program.

**logical.py** defines the logical layer. It's an abstract interface to a key/value store.
- LogicalBase provides the API for logical updates (like get, set, and commit) and defers to a concrete subclass to implement the updates themselves. It also manages storage locking and dereferencing internal nodes.
- ValueRef is a Python object that refers to a binary blob stored in the database. The indirection lets us avoid loading the entire data store into memory all at once.

**binary_tree.py** defines a concrete binary tree algorithm underneath the logical interface.

- BinaryTree provides a concrete implementation of a binary tree, with methods for getting, inserting, and deleting key/value pairs. BinaryTree represents an immutable tree; updates are performed by returning a new tree which shares common structure with the old one.
- BinaryNode implements a node in the binary tree.
- BinaryNodeRef is a specialised ValueRef which knows how to serialise and deserialise a BinaryNode.

**physical.py** defines the physical layer. The Storage class provides persistent, (mostly) append-only record storage.
