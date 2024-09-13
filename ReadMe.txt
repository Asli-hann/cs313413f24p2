TestIterator.java

1. Imports
Added import java.lang.* to include the required language packages.

2. setUp() Method
The code uses an ArrayList by default, but switching to a LinkedList results
in only minor differences.
ArrayList is faster for random access, while LinkedList is faster for
frequent insertions/removals in the middle of the list.

3. testNonempty() Method
Updated the expected values in the assertions to correctly match the list elements.

4. testRemove() Method
If list.remove(Integer.valueOf(77)) is used inside the loop, we get a
ConcurrentModificationException error due to modifying the list directly
while using an iterator, that is why it is safer to use an iterator while
removing the element.
After removing all occurrences of 77, assertEquals(List.of(33,44,55,66),list)
added to check if the final version of the list is matching with the expectation.

5. testAverageValues() Method
An iterator and a while loop added to compute the mean.

TestList.java
1. setUp() Method
ArrayList is typically faster than LinkedList for random access operations
because it allows direct indexing. In this test case ArrayList is 1ms faster.

2. testSizeNonEmpty()
Changed list.isEmpty() to return false, set the expected list size to 1,
and the expected value at index 0 to 77.

3. testContains()
Added assertFalse() and assertTrue() to check if the list contains the
integer 77 before and after adding it.

4. testAddMultiple()
Updated the expected size of the list and verified the first and
last indices of the value 77.

5. testAddMultiple2()
Similar to testAddMultiple(), updated the expected values for size,
indices, and specific elements.

6. testRemoveObject()
Updated the expected values to compare the list before and after removing
specific items using both index-based and object-based removal.

7.testContainsAll()
Used list.containsAll() to verify that the
necessary elements are present and absent in the list.

8. testAddAll()
Added all items in the assertions to the list using the addAll() method.

9. testRemoveAll()
Removed all items except the ones in the assertion using removeAll().

10. testRetainAll()
Used retainAll() to remove all elements from the list except for 77.

11. testSet()
Replaced the values at specific indices using the set() method to
match the expected ones.

12. testSubList()
Corrected the indices in the subList() method to match the expected output.

TestPerformance.java

1. The performance of the code when the SIZE is 10 and a 100 is almost
the same for each test, so the difference is not noticeable. But, when the SIZE
is increased to 1000 the performance difference between the two access and Add/Remove
methods becomes significant. When the SIZE reaches 10,000 the total runtime
exceeds 10 seconds. At this point, it is clear that if the goal is to access
elements it is much more efficient to use ArrayList rather than LinkedList. However,
if the goal is to Add/Remove elements from a list, it is better to use LinkedList.
If the size of the list is fixed and below 100, it doesn't matter much
which one to use, but as the size increases, it significantly affects performance.
Therefore depending on the operation being performed, the type of the list
should be chosen accordingly.

2. To refactor the code, two helper methods (dryAccess and dryAddRemove) were added
to avoid duplication by encapsulating the logic for adding/removing and accessing
elements.

3. When the repetition count (REPS) is below 10,000, its effect on runtime is not
noticeable. When REPS is 100,000, the difference becomes more noticeable but is
unlikely to cause a runtime issue. However, when REPS exceeds 1,000,000, its
impact on runtime becomes much more significant. At this point, it is important
to carefully decide whether to use ArrayList or LinkedList depending on the
operations that need to be performed.

