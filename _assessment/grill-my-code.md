## Grill My Code

> **Generated:** 2026-05-05 12:54:08 UTC
> **Commits reviewed:** `22df531` → `f60f6f7`

> **Files assessed:** `src/LinkedList.cpp`, `src/LinkedList.h`, `src/main.cpp`

---

## Recall

_These questions check your knowledge of what specific parts of your code do._

1. **`src/LinkedList.cpp`**
   ```
   head = nullptr;
   ```
   What does the constructor for `LinkedList` do to the `head` pointer?

2. **`src/LinkedList.cpp`**
   ```
   BugNode* next = current->next;
   delete current;
   current = next;
   ```
   What is happening to each node within the `LinkedList` destructor?

3. **`src/LinkedList.cpp`**
   ```
   BugNode* node = new BugNode;
   node->data = bug;
   node->next = nullptr;
   ```
   What is being created each time `addBug` is called?

4. **`src/LinkedList.cpp`**
   ```
   if (head == nullptr) {
       head = node;
       return;
   }
   ```
   What does the `addBug` method do if the list is empty?

5. **`src/LinkedList.cpp`**
   ```
   while (current != nullptr && current->data.id != bugId) {
       prev = current;
       current = current->next;
   }
   ```
   What condition causes the loop in `deleteBug` to stop?

6. **`src/LinkedList.cpp`**
   ```
   if (prev == nullptr) {
       head = current->next;
   }
   ```
   What happens if `deleteBug` finds the bug to delete at the head of the list?

7. **`src/LinkedList.cpp`**
   ```
   if (current->data.id == bugId) {
       return &current->data;
   }
   ```
   What does `searchBug` return if it finds a bug with a matching ID?

8. **`src/LinkedList.cpp`**
   ```
   for (int i = 0; i < current->data.commentCount; i++) {
       std::cout << "Comment " << i + 1 << ": "
                 << current->data.comments[i] << std::endl;
   }
   ```
   What does the loop in `display` output for each bug?

9. **`src/LinkedList.cpp`**
   ```
   while (current->next != nullptr) {
       if (current->data.id > current->next->data.id) {
           Bug temp = current->data;
           current->data = current->next->data;
           current->next->data = temp;
           swapped = true;
       }
       current = current->next;
   }
   ```
   What is the purpose of the inner loop in `sortById`?

10. **`src/LinkedList.cpp`**
    ```
    if (!head) return;
    ```
    What does `sortById` do if the list is empty?

11. **`src/LinkedList.cpp`**
    ```
    BugNode* current = head;
    while (current != nullptr) {
        file << current->data.id << "|"
    ```
    What does `saveToFile` do with each node in the list?

12. **`src/LinkedList.h`**
    ```
    std::string comments[10];
    int commentCount;
    ```
    What is the role of the `comments` array and `commentCount` in the `Bug` struct?

13. **`src/main.cpp`**
    ```
    LinkedList list;
    ```
    What object is being created at the start of `main`?

14. **`src/main.cpp`**
    ```
    list.loadFromFile("../docs/bugFile.txt");
    ```
    What does the call to `loadFromFile` do at the beginning of `main`?

15. **`src/main.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    What does this initialization assign to `b1`?

16. **`src/main.cpp`**
    ```
    list.addBug(b1);
    ```
    What effect does calling `addBug(b1)` have on the linked list?

17. **`src/main.cpp`**
    ```
    list.sortById();
    ```
    What is the expected result after this line is executed?

18. **`src/main.cpp`**
    ```
    list.deleteBug(3);
    ```
    What happens to the bug with ID 3 after this line in `main`?

19. **`src/main.cpp`**
    ```
    Bug* found = list.searchBug(2);
    ```
    What is stored in `found` after this call?

20. **`src/main.cpp`**
    ```
    list.saveToFile("../output/bugFile.txt");
    ```
    What does this statement do at the end of `main`?

## Comprehension

_These questions ask you to explain why or how particular choices in your code work the way they do._

21. **`src/LinkedList.cpp`**
    ```
    while (current->next != nullptr) {
        current = current->next;
    }
    ```
    Why is this loop used in `addBug` instead of inserting at the head?

22. **`src/LinkedList.cpp`**
    ```
    BugNode* prev = nullptr;
    ```
    Why is `prev` initialized to `nullptr` at the start of `deleteBug`?

23. **`src/LinkedList.cpp`**
    ```
    if (current == nullptr) {
        return;
    }
    ```
    Why does `deleteBug` immediately return if no matching bug is found?

24. **`src/LinkedList.cpp`**
    ```
    while (current != nullptr) {
        if (current->data.id == bugId) {
            return &current->data;
        }
        current = current->next;
    }
    ```
    Why does `searchBug` return a pointer rather than a copy of the bug?

25. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        std::cout << "Comment " << i + 1 << ": "
                  << current->data.comments[i] << std::endl;
    }
    ```
    Why is `commentCount` used as the loop bound instead of the fixed comment array size?

26. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    Why does the sorting algorithm swap `Bug` structs instead of rearranging the nodes themselves?

27. **`src/LinkedList.cpp`**
    ```
    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;

        if (bug.commentCount < 10) {
            bug.comments[bug.commentCount++] = comment;
        }
    }
    ```
    Why is there a check for `bug.commentCount < 10` during comment loading?

28. **`src/LinkedList.cpp`**
    ```
    file << current->data.id << "|"
         << current->data.date << "|"
         << current->data.briefDesc << "|"
         << current->data.detailedDesc << "|"
         << current->data.status << "|"
         << current->data.severity << "|";
    ```
    Why are bug fields written to the file separated by `|`?

29. **`src/LinkedList.cpp`**
    ```
    file << "||\n";
    ```
    Why does `saveToFile` include `"||\n"` after writing comments?

30. **`src/LinkedList.h`**
    ```
    BugNode* head = nullptr;
    ```
    Why is `head` defined as a private member of the `LinkedList` class?

31. **`src/main.cpp`**
    ```
    list.display();
    ```
    Why is `display` called after sorting and deleting operations?

32. **`src/main.cpp`**
    ```
    if (found) {
        std::cout << "\nFound Bug ID 2:\n";
        std::cout << found->briefDesc << std::endl;
    }
    ```
    Why is there a conditional check on `found` before printing bug information?

33. **`src/main.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    Why are bugs initialized using brace-enclosed lists in `main`?

34. **`src/LinkedList.cpp`**
    ```
    std::ifstream file(filename);

    if (!file) {
        std::cout << "File not found.\n";
        return;
    }
    ```
    Why is there a check for file existence before loading in `loadFromFile`?

35. **`src/LinkedList.cpp`**
    ```
    std::ofstream file(filename);
    ```
    Why does `saveToFile` create a new output file stream each time it's called?

## Analysis

_These questions require you to trace execution, reason about logic, or identify possible issues._

36. **`src/LinkedList.cpp`**
    ```
    delete current;
    ```
    What could happen if `deleteBug` is called with an ID not present in the list?

37. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId)
    ```
    What happens if you call `searchBug` on an empty list?

38. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        std::cout << "Comment " << i + 1 << ": "
                  << current->data.comments[i] << std::endl;
    }
    ```
    How would the output change if `commentCount` is incorrectly set higher than the actual number of comments?

39. **`src/LinkedList.cpp`**
    ```
    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;
    ```
    What happens if a bug in the file has no comments between the last field and the `||` marker?

40. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;
    node->data = bug;
    node->next = nullptr;
    ```
    What happens if `addBug` is called repeatedly without deleting the list?

41. **`src/LinkedList.cpp`**
    ```
    while (current->next != nullptr) {
        if (current->data.id > current->next->data.id) {
    ```
    How does the sort algorithm behave if IDs are already sorted?

42. **`src/LinkedList.cpp`**
    ```
    while (current->next != nullptr) {
        if (current->data.status > current->next->data.status) {
    ```
    How does `sortByStatus` determine the order of bugs?

43. **`src/LinkedList.cpp`**
    ```
    if (!head) return;
    ```
    What is the effect of calling `sortById` or `sortByStatus` on a single-node list?

44. **`src/LinkedList.cpp`**
    ```
    file << current->data.id << "|"
    ```
    What could happen if a bug's field contains the `|` character?

45. **`src/LinkedList.cpp`**
    ```
    bug.comments[bug.commentCount++] = comment;
    ```
    What happens if a bug in the file has more than 10 comments?

46. **`src/LinkedList.cpp`**
    ```
    head = nullptr;
    ```
    What is the effect of setting `head` to nullptr in the destructor?

47. **`src/main.cpp`**
    ```
    Bug* found = list.searchBug(2);
    ```
    What value will `found` have if no bug with ID 2 exists?

48. **`src/main.cpp`**
    ```
    list.saveToFile("../output/bugFile.txt");
    ```
    What will the output file contain if the list is empty when `saveToFile` is called?

49. **`src/main.cpp`**
    ```
    list.deleteBug(3);
    ```
    What happens if you try to delete a bug that was already deleted in a previous operation?

## Evaluation

_These questions ask you to judge design decisions, tradeoffs, or rationale._

50. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    What are the implications of sorting by swapping bug data rather than linked list nodes in terms of performance and memory usage?

---

<sub>Generated by [grill-my-code](https://github.com/NSCC-ITC-Assessment/GrillMyCode) · gpt-4.1 via github-models · main</sub>