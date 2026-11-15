1. For every function you wrote (TODO 1 to 19), explain in your own words what it does and give its time complexity in terms of n, the number of scenes. One short paragraph each.

TODO1: It runs in O(1) time because there are at most 3 choices.
TODO2: It runs across the whole tree. It runs in O(n) time.
TODO3: Checks if numChoices_ equals 0. It runs in O(1) time.
TODO4: Returns choices_[index] if the index is valid, or nullptr if invalid. It runs in O(1) time.
TODO5: Stores a child pointer into choices_[index] if the index is valid. It runs in O(1) time.
TODO6: Repeatedly counts 1 for the scene with all other child scenes. It runs in O(n) time.
TODO7: Repeatedly returns 1 at each leaf. It runs in O(n) time.
TODO8: Repeatedly finds the largest child height and adds 1. It runs in O(n) time.
TODO9: Deletes root_ to free the entire tree. It runs in O(n) time.
TODO10: It reads START_HP, calls readScene, and sets the tree root. It runs in O(n) time.
TODO11: Repeatedly reads all child scenes. It runs in O(n) time.
TODO12: It runs in O(1) time relative to the number of scenes.
TODO13: It runs in O(n) time for walking the path, or O(n^2) worst-case if searching a growing bag at every step.
TODO14: Calls countScenes(), countEndings(), and height(). It runs in O(n) time.
TODO15: Calls printEndings starting at the root. It runs in O(n) time.
TODO16: Repeatedly walks from choice 1 to choice 3. It runs in O(n) time.
TODO17: Loops down one path until dying or reaching an ending. It runs in O(n) time.
TODO18: Repeatedly visits each scene once and runs in O(n) time.
TODO19: Calls bestLoot from the root. It runs in O(n) time.


2. Why does each scene allocate exactly numChoices slots instead of declaring Scene<T>* choices[3]? What does an ending hold in choices_, and why?

A fixed array of 3 wastes space when a scene has fewer choices. An ending has 0 choices, so choices_ contains nullptr.


3. Walk through your Scene destructor. What gets deleted, and in what order? What would go wrong if choices_ were deleted first?

First, delete data_ frees the Moment. Then, a loop deletes each child scene choices_[i]. Finally, delete[] choices_ frees the array. Deleting choices_ first would lose the child pointers and the tree would leak.


4. Show the path greedy took and the path optimal took on your story, with the loot for each. Explain why greedy lost. If greedy did not lose, change your story until it does, and explain what you changed.

Greedy took 1-1 for 18 loot and died with -6 HP. Optimal took 2-2-2-2-1 for 27 loot and survived with 10 HP. Greedy lost because it picked loot right into a spike trap.


5. bestLoot tries every path, yet it runs in O(n) time. Explain why it is not exponential, using what you know about paths and leaves in a tree.

A tree has no cycles, and each scene has one parent, so there is only one path to each node.


6. Which List methods does your game use, and why? What does one search cost as the bag grows?

The game uses search to avoid duplicates, addFront to store new items, size to show the count, and print to display the bag. Searching a bag of k items costs O(k) time.