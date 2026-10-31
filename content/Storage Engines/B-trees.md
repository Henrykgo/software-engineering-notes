B-trees are balanced tree based storage structures that organise sorted keys and their values into fixed size pages, enabling efficient look up and updates.

![[Screenshot 2026-10-19 at 14.47.27.png]]
## How it works?
1. The disk is organised into fixed-size pages. Each page can reference another page by its location on disk.
2. A lookup starts at the root, follows the reference for the range containing the key we are looking for and repeats until we find the leaf page containing the key and its value(or reference to the data). This walks takes only a few steps O(log `n`), because each page usually holds hundreds of references (branching factor) so the tree is shallow.
3. To update a value for an existing key(update in plate), you search for the leaf page containing the key and overwrite that page on disk with the new value.
4. To add a new key, you find appropriate leaf page to add the new key, if the page is full, it splits into 2, and the parent is updated to account for the new pages.

### Making it reliable
A page split will overwrite several pages, so a crash midway can cause a corrupted tree (e.g. an orphaned page that is not a child of any parent). So before every b-tree modification the changes are appended first to a [[Write-ahead log]], which ensures that if a crash happens it can be restored to a consistent state.

### Used in?
Standard index implementation in relational databases (e.g. PostgreSQL, MySQL, SQLite, Oracle, SQL Server.)

### Source
- DDIA (Chapter 4. Storage and retrieval) #source/ddia/ch4
