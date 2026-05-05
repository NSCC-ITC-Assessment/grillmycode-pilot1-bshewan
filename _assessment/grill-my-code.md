## Grill My Code

> **Generated:** 2026-05-05 13:15:25 UTC
> **Commits reviewed:** `22df531` → `f254d0b`

> **Files assessed:** `src/LinkedList.cpp`, `src/LinkedList.h`, `src/main.cpp`

---

## Recall

_These questions check your knowledge of what specific parts of your code do._

1. **`src/LinkedList.cpp`**
   ```
   head = nullptr;
   ```
   What does the `LinkedList` constructor initialize when a new `LinkedList` object is created?
2. **`src/LinkedList.cpp`**
   ```
   BugNode* current = head;
   while (current != nullptr) {
       BugNode* next = current->next;
       delete current;
       current = next;
   }
   ```
   What happens to the memory allocated for nodes when the `LinkedList` destructor is called?
3. **`src/LinkedList.cpp`**
   ```
   if (head == nullptr) {
       head = node;
       return;
   }
   ```
   What condition causes `addBug` to immediately set `head` and return?
4. **`src/LinkedList.cpp`**
   ```
   while (current->next != nullptr) {
       current = current->next;
   }
   current->next = node;
   ```
   Where is a new bug added within the list when `addBug` is called and the list is not empty?
5. **`src/LinkedList.cpp`**
   ```
   while (current != nullptr && current->data.id != bugId) {
       prev = current;
       current = current->next;
   }
   ```
   What is the purpose of this loop in the `deleteBug` method?
6. **`src/LinkedList.cpp`**
   ```
   if (current == nullptr) {
       return;
   }
   ```
   What does `deleteBug` do if no node with the given `bugId` is found?
7. **`src/LinkedList.cpp`**
   ```
   if (prev == nullptr) {
       head = current->next;
   }else {
       prev->next = current->next;
   }
   ```
   How is the linked list adjusted when deleting a node at the head versus elsewhere?
8. **`src/LinkedList.cpp`**
   ```
   if (current->data.id == bugId) {
       return &current->data;
   }
   ```
   What value is returned by `searchBug` when a bug with the specified ID is found?
9. **`src/LinkedList.cpp`**
   ```
   std::cout << "ID: " << current->data.id << std::endl;
   ```
   Which bug field is printed first in the `display` method?
10. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        std::cout << "Comment " << i + 1 << ": "
                  << current->data.comments[i] << std::endl;
    }
    ```
    What determines how many comments are printed for each bug in the `display` method?
11. **`src/LinkedList.cpp`**
    ```
    if (!head) return;
    ```
    What check is performed at the beginning of both `sortById` and `sortByStatus`?
12. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    What operation is performed when two bugs are out of order during sorting?
13. **`src/LinkedList.cpp`**
    ```
    std::ifstream file(filename);

    if (!file) {
        std::cout << "File not found.\n";
        return;
    }
    ```
    What happens if the file specified in `loadFromFile` cannot be opened?
14. **`src/LinkedList.cpp`**
    ```
    getline(ss, bug.date, '|');
    getline(ss, bug.briefDesc, '|');
    ```
    Which bug fields are read from each line of the file in `loadFromFile` after reading `id`?
15. **`src/LinkedList.cpp`**
    ```
    if (bug.commentCount < 10) {
        bug.comments[bug.commentCount++] = comment;
    }
    ```
    What prevents more than 10 comments from being added to a bug when loading from file?
16. **`src/LinkedList.cpp`**
    ```
    file << current->data.id << "|"
         << current->data.date << "|"
         ...
         << "||\n";
    ```
    How are bug fields separated in the output file when using `saveToFile`?
17. **`src/LinkedList.cpp`**
    ```
    file.close();
    ```
    What happens at the end of both `loadFromFile` and `saveToFile`?
18. **`src/LinkedList.h`**
    ```
    BugNode* head = nullptr;
    ```
    What member variable does the `LinkedList` class use to keep track of the first node?
19. **`src/LinkedList.h`**
    ```
    std::string comments[10];
    int commentCount;
    ```
    How are bug comments stored in the `Bug` struct?
20. **`src/main.cpp`**
    ```
    LinkedList list;
    ```
    What type of object is created at the start of the `main` function?
21. **`src/main.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    What information is assigned to `b1` upon initialization?
22. **`src/main.cpp`**
    ```
    list.addBug(b1);
    list.addBug(b2);
    list.addBug(b3);
    list.addBug(b4);
    list.addBug(b5);
    ```
    What happens to the list after these five calls to `addBug`?
23. **`src/main.cpp`**
    ```
    list.sortById();
    ```
    What operation is performed on the list before displaying bugs sorted by ID?
24. **`src/main.cpp`**
    ```
    list.deleteBug(3);
    ```
    What does this line attempt to do to the linked list?
25. **`src/main.cpp`**
    ```
    Bug* found = list.searchBug(2);
    if (found) {
        std::cout << "\nFound Bug ID 2:\n";
        std::cout << found->briefDesc << std::endl;
    }
    ```
    What bug information is printed if a bug with ID 2 is found?

## Comprehension

_These questions ask you to explain why or how particular choices in your code work the way they do._

26. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;
    node->data = bug;
    node->next = nullptr;
    ```
    Why do you create a new `BugNode` and set its `next` to `nullptr` before adding it to the list in `addBug`?
27. **`src/LinkedList.cpp`**
    ```
    delete current;
    ```
    Why is it necessary to explicitly delete nodes in the destructor rather than relying on automatic memory management?
28. **`src/LinkedList.cpp`**
    ```
    while (current != nullptr && current->data.id != bugId) {
        prev = current;
        current = current->next;
    }
    ```
    How does this loop help locate the node to be deleted, and why is `prev` tracked?
29. **`src/LinkedList.cpp`**
    ```
    return &current->data;
    ```
    Why does `searchBug` return a pointer to the bug data instead of the node itself or a copy?
30. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        std::cout << "Comment " << i + 1 << ": "
                  << current->data.comments[i] << std::endl;
    }
    ```
    How does this loop ensure that only valid comments are displayed for each bug?
31. **`src/LinkedList.cpp`**
    ```
    do {
        swapped = false;
        BugNode* current = head;
        while (current->next != nullptr) {
            if (current->data.id > current->next->data.id) {
                Bug temp = current->data;
                current->data = current->next->data;
                current->next->data = temp;
                swapped = true;
            }
            current = current->next;
        }
    }while (swapped);
    ```
    Why do you use a do-while loop for the sorting methods instead of a single pass?
32. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    Why do you swap the `data` field of nodes instead of rearranging the nodes themselves during sorting?
33. **`src/LinkedList.cpp`**
    ```
    getline(ss, token, '|');
    bug.id = stoi(token);
    ```
    Why do you read the first token and convert it to an integer in `loadFromFile`?
34. **`src/LinkedList.cpp`**
    ```
    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;
        if (bug.commentCount < 10) {
            bug.comments[bug.commentCount++] = comment;
        }
    }
    ```
    How does this loop ensure that no more than 10 comments are added, and what happens if the comment is empty?
35. **`src/LinkedList.cpp`**
    ```
    file << current->data.id << "|"
         << current->data.date << "|"
         << current->data.briefDesc << "|"
         << current->data.detailedDesc << "|"
         << current->data.status << "|"
         << current->data.severity << "|";
    ```
    Why is each bug field separated by a `|` when saving to file?
36. **`src/LinkedList.cpp`**
    ```
    file << "||\n";
    ```
    Why is `||\n` written at the end of each bug entry in the output file?
37. **`src/LinkedList.h`**
    ```
    std::string comments[10];
    int commentCount;
    ```
    Why does the `Bug` struct use a fixed-size array for comments and an integer for the count?
38. **`src/LinkedList.h`**
    ```
    BugNode* next;
    ```
    What role does the `next` pointer play in the `BugNode` struct?
39. **`src/LinkedList.h`**
    ```
    void sortByStatus();
    ```
    How does `sortByStatus` determine the sorting order for bugs in the list?
40. **`src/main.cpp`**
    ```
    list.loadFromFile("../docs/bugFile.txt");
    ```
    Why does the program load bugs from a file before adding new bugs in `main`?
41. **`src/main.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    Why does the bug initialization list specify fields in a particular order?
42. **`src/main.cpp`**
    ```
    list.sortById();
    std::cout << "\nSorted by ID:\n";
    list.display();
    ```
    Why is `display` called after sorting by ID, and what would happen if it was called before sorting?
43. **`src/main.cpp`**
    ```
    Bug* found = list.searchBug(2);
    if (found) {
        std::cout << "\nFound Bug ID 2:\n";
        std::cout << found->briefDesc << std::endl;
    }
    ```
    Why is the result of `searchBug` checked before printing the bug description?
44. **`src/main.cpp`**
    ```
    list.saveToFile("../output/bugFile.txt");
    ```
    Why is the list saved to a file at the end of the `main` function?

## Analysis

_These questions require tracing execution, reasoning about logic, or identifying issues in the code._

45. **`src/LinkedList.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    If only a single string is specified for `comments` in this initialization, how does the code handle the rest of the array and `commentCount`?
46. **`src/LinkedList.cpp`**
    ```
    BugNode* current = head;
    while (current != nullptr) {
        BugNode* next = current->next;
        delete current;
        current = next;
    }
    ```
    What would happen if a node in the list pointed to itself instead of `nullptr`?
47. **`src/LinkedList.cpp`**
    ```
    while (current->next != nullptr) {
        current = current->next;
    }
    current->next = node;
    ```
    What is the time complexity of adding a bug to the end of the list, and how does it scale with the list's size?
48. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId)
    ```
    How does the `searchBug` method behave if there are multiple bugs with the same ID in the list?
49. **`src/LinkedList.cpp`**
    ```
    if (current == nullptr) {
        return nullptr;
    }
    ```
    How does the `searchBug` method communicate failure to find a bug, and how is this handled in `main`?
50. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    What are the potential drawbacks of swapping bug data instead of nodes, especially regarding pointers or references to bugs elsewhere in the code?
51. **`src/LinkedList.cpp`**
    ```
    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;
        if (bug.commentCount < 10) {
            bug.comments[bug.commentCount++] = comment;
        }
    }
    ```
    What happens if the input file contains more than 10 comments for a bug?
52. **`src/LinkedList.cpp`**
    ```
    file << "||\n";
    ```
    How does this output affect the loading logic when reading from the file?
53. **`src/LinkedList.h`**
    ```
    BugNode* head = nullptr;
    ```
    If multiple lists are created, how does each list maintain its own set of bugs?
54. **`src/main.cpp`**
    ```
    list.deleteBug(3);
    ```
    What happens to the memory and pointers in the list when bug ID 3 is deleted?
55. **`src/main.cpp`**
    ```
    list.sortByStatus();
    ```
    If multiple bugs have the same status, how are they ordered after sorting?

## Evaluation

_These questions ask you to judge design decisions, tradeoffs, or rationale in the code._

56. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;
    ```
    What are the benefits and risks of using dynamic memory allocation for each node in the linked list?
57. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    What are the tradeoffs between swapping bug data versus rearranging node pointers during sorting?
58. **`src/LinkedList.cpp`**
    ```
    std::string comments[10];
    ```
    How does using a fixed-size array for comments impact flexibility and memory usage compared to using a dynamic container?
59. **`src/LinkedList.cpp`**
    ```
    void sortById();
    void sortByStatus();
    ```
    What are the advantages and disadvantages of using bubble sort for sorting bugs in the linked list?
60. **`src/LinkedList.cpp`**
    ```
    Bug* searchBug(int bugId);
    ```
    What are the implications of returning a pointer to internal data from `searchBug` for encapsulation and safety?
61. **`src/LinkedList.cpp`**
    ```
    void loadFromFile(const std::string& filename);
    ```
    How might error handling in `loadFromFile` affect the robustness of the program, and what alternatives could improve it?
62. **`src/LinkedList.cpp`**
    ```
    void saveToFile(const std::string& filename) const;
    ```
    What are the advantages of separating file input/output from the core list operations?
63. **`src/LinkedList.h`**
    ```
    BugNode* head = nullptr;
    ```
    Why might you choose a singly linked list for this application instead of a doubly linked list?
64. **`src/LinkedList.h`**
    ```
    struct Bug { ... };
    ```
    What benefits does using a struct for bug representation offer, and what limitations might arise?
65. **`src/main.cpp`**
    ```
    LinkedList list;
    ```
    What design advantages does using a dedicated `LinkedList` class provide for managing bug reports?

---

<sub>Generated by [grill-my-code](https://github.com/NSCC-ITC-Assessment/GrillMyCode) · gpt-4.1 via github-models · main</sub>