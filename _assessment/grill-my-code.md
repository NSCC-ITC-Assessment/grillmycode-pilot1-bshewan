## Grill My Code

> **Generated:** 2026-05-05 13:33:04 UTC
> **Commits reviewed:** `22df531` → `15edf03`

> **Files assessed:** `src/LinkedList.cpp`, `src/LinkedList.h`, `src/main.cpp`

---

## Recall

_These questions check your knowledge of what specific parts of your code do._

1. **`src/LinkedList.cpp`**
    ```
    BugNode* current = head;

    while (current != nullptr) {
        BugNode* next = current->next;
        delete current;
        current = next;
    }

    head = nullptr;
    ```
    What does the destructor `~LinkedList` do to the linked list when called?

2. **`src/LinkedList.cpp`**
    ```
    void LinkedList::addBug(const Bug& bug) {

        BugNode* node = new BugNode;

        node->data = bug;
        node->next = nullptr;

        if (head == nullptr) {
            head = node;
            return;
        }

        BugNode* current = head;
        while (current->next != nullptr) {
            current = current->next;
        }

        current->next = node;
    }
    ```
    What is the effect of calling `addBug` with a new `Bug` when the list is empty?

3. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId) {

        BugNode* current = head;

        while (current != nullptr) {
            if (current->data.id == bugId) {
                return &current->data;
            }
            current = current->next;
        }

        return nullptr;
    }
    ```
    What does `searchBug` return if no bug with `bugId` is found?

4. **`src/LinkedList.cpp`**
    ```
    void LinkedList::deleteBug(int bugId) {
        BugNode* current = head;
        BugNode* prev = nullptr;

        while (current != nullptr && current->data.id != bugId) {
            prev = current;
            current = current->next;
        }

        if (current == nullptr) {
            return;
        }

        if (prev == nullptr) {
            head = current->next;
        }else {
            prev->next = current->next;
        }
        delete current;
    }
    ```
    What happens when you call `deleteBug` with a `bugId` that does not exist in the list?

5. **`src/LinkedList.cpp`**
    ```
    void LinkedList::display() const{

        BugNode* current = head;

        while (current != nullptr) {
            std::cout << "ID: " << current->data.id << std::endl;
            std::cout << "Date: " << current->data.date << std::endl;
            std::cout << "Brief: " << current->data.briefDesc << std::endl;
            std::cout << "Detail: " << current->data.detailedDesc << std::endl;
            std::cout << "Status: " << current->data.status << std::endl;
            std::cout << "Severity: " << current->data.severity << std::endl;

            for (int i = 0; i < current->data.commentCount; i++) {
                std::cout << "Comment " << i + 1 << ": "
                          << current->data.comments[i] << std::endl;
            }
            std::cout << "-------------------------" << std::endl;

            current = current->next;
        }

    }
    ```
    What does the `display` function print for each bug in the list?

6. **`src/LinkedList.cpp`**
    ```
    void LinkedList::sortById() {
        if (!head) return;

        bool swapped;
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
    }
    ```
    What is the result of calling `sortById` on the linked list?

7. **`src/LinkedList.cpp`**
    ```
    void LinkedList::sortByStatus() {
        if (!head) return;

        bool swapped;
        do {
            swapped = false;
            BugNode* current = head;

            while (current->next != nullptr) {
                if (current->data.status > current->next->data.status) {

                    Bug temp = current->data;
                    current->data = current->next->data;
                    current->next->data = temp;

                    swapped = true;
                }
                current = current->next;
            }
        }while (swapped);
    }
    ```
    What criterion does `sortByStatus` use to arrange bugs in the list?

8. **`src/LinkedList.cpp`**
    ```
    void LinkedList::loadFromFile(const std::string& filename) {
        std::ifstream file(filename);

        if (!file) {
            std::cout << "File not found.\n";
            return;
        }

        std::string line;

        while (getline(file, line)) {
            std::stringstream ss(line);
            std::string token;
            std::string comment;

            Bug bug;
            getline(ss, token, '|');
            bug.id = stoi(token);

            getline(ss, bug.date, '|');
            getline(ss, bug.briefDesc, '|');
            getline(ss, bug.detailedDesc, '|');
            getline(ss, bug.status, '|');
            getline(ss, bug.severity, '|');

           bug.commentCount = 0;

            while (getline(ss, comment, '|')) {
                if (comment.empty()) break;

                if (bug.commentCount < 10) {
                    bug.comments[bug.commentCount++] = comment;
                }
            }

            addBug(bug);
        }
        file.close();
    }
    ```
    What does `loadFromFile` do with each line it reads from the file?

9. **`src/LinkedList.cpp`**
    ```
    void LinkedList::saveToFile(const std::string& filename) const {
        std::ofstream file(filename);

        BugNode* current = head;

        while (current != nullptr) {
            file << current->data.id << "|"
                 << current->data.date << "|"
                 << current->data.briefDesc << "|"
                 << current->data.detailedDesc << "|"
                 << current->data.status << "|"
                 << current->data.severity << "|";

            for (int i = 0; i < current->data.commentCount; i++) {
                file << current->data.comments[i] << "|";
            }
            file << "||\n";
            current = current->next;
        }

        file.close();
    };
    ```
    What does the `saveToFile` function output for each bug in the linked list?

10. **`src/main.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    Bug b2 = {2, "2026-04-25", "Login bug", "Can't login", "IN PROGRESS", "CRITICAL", "Working on it"};
    Bug b3 = {3, "2026-04-26", "UI issue", "Button broken", "WAITING", "LOW", "Minor"};
    Bug b4 = {4, "2026-04-27", "Slow app", "Performance lag", "OPEN", "MEDIUM", "Investigating"};
    Bug b5 = {5, "2026-04-28", "Security", "Vulnerability", "CLOSED", "CRITICAL", "Fixed"};

    list.addBug(b1);
    list.addBug(b2);
    list.addBug(b3);
    list.addBug(b4);
    list.addBug(b5);
    ```
    What is the purpose of creating and adding these five bugs in `main`?

## Comprehension

_These questions ask you to explain why or how particular choices in your code work the way they do._

11. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;

    node->data = bug;
    node->next = nullptr;

    if (head == nullptr) {
        head = node;
        return;
    }

    BugNode* current = head;
    while (current->next != nullptr) {
        current = current->next;
    }

    current->next = node;
    ```
    Why did you implement `addBug` so that new bugs are always appended at the end of the list?

12. **`src/LinkedList.cpp`**
    ```
    if (prev == nullptr) {
        head = current->next;
    }else {
        prev->next = current->next;
    }
    delete current;
    ```
    In `deleteBug`, why do you treat the case where `prev` is `nullptr` differently from when it is not?

13. **`src/LinkedList.cpp`**
    ```
    if (!head) return;

    bool swapped;
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
    Why did you choose to swap the `Bug` data inside nodes instead of rearranging the node pointers in `sortById`?

14. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        std::cout << "Comment " << i + 1 << ": "
                  << current->data.comments[i] << std::endl;
    }
    ```
    How does the `display` function ensure that only valid comments are printed for each bug?

15. **`src/LinkedList.cpp`**
    ```
    getline(ss, token, '|');
    bug.id = stoi(token);
    ...
    bug.commentCount = 0;

    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;

        if (bug.commentCount < 10) {
            bug.comments[bug.commentCount++] = comment;
        }
    }
    ```
    Why do you check for `comment.empty()` before adding comments in `loadFromFile`?

16. **`src/LinkedList.cpp`**
    ```
    void LinkedList::saveToFile(const std::string& filename) const {
        std::ofstream file(filename);

        BugNode* current = head;

        while (current != nullptr) {
            file << current->data.id << "|"
                 << current->data.date << "|"
                 << current->data.briefDesc << "|"
                 << current->data.detailedDesc << "|"
                 << current->data.status << "|"
                 << current->data.severity << "|";

            for (int i = 0; i < current->data.commentCount; i++) {
                file << current->data.comments[i] << "|";
            }
            file << "||\n";
            current = current->next;
        }

        file.close();
    };
    ```
    How does `saveToFile` guarantee that the output file can be parsed by `loadFromFile` later?

17. **`src/LinkedList.cpp`**
    ```
    void LinkedList::sortByStatus() {
        if (!head) return;

        bool swapped;
        do {
            swapped = false;
            BugNode* current = head;

            while (current->next != nullptr) {
                if (current->data.status > current->next->data.status) {

                    Bug temp = current->data;
                    current->data = current->next->data;
                    current->next->data = temp;

                    swapped = true;
                }
                current = current->next;
            }
        }while (swapped);
    }
    ```
    Why does the sort-by-status algorithm rely on the comparison `current->data.status > current->next->data.status`?

18. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId) {

        BugNode* current = head;

        while (current != nullptr) {
            if (current->data.id == bugId) {
                return &current->data;
            }
            current = current->next;
        }

        return nullptr;
    }
    ```
    How does `searchBug` guarantee that only one bug with a given id will be returned?

19. **`src/LinkedList.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    Why does the bug struct initialization in `main` only provide one comment, given that the struct can hold up to 10?

20. **`src/LinkedList.cpp`**
    ```
    head = nullptr;
    ```
    Why is it necessary to set `head` to `nullptr` at the end of the destructor?

## Analysis

_These questions require tracing execution, reasoning about logic, or identifying issues in the code._

21. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;

    node->data = bug;
    node->next = nullptr;

    if (head == nullptr) {
        head = node;
        return;
    }

    BugNode* current = head;
    while (current->next != nullptr) {
        current = current->next;
    }

    current->next = node;
    ```
    What happens if you call `addBug` multiple times in succession, and how does the list structure change?

22. **`src/LinkedList.cpp`**
    ```
    BugNode* current = head;
    BugNode* prev = nullptr;

    while (current != nullptr && current->data.id != bugId) {
        prev = current;
        current = current->next;
    }

    if (current == nullptr) {
        return;
    }

    if (prev == nullptr) {
        head = current->next;
    }else {
        prev->next = current->next;
    }
    delete current;
    ```
    If you delete the head bug in the list, how does the linked list structure change afterwards?

23. **`src/LinkedList.cpp`**
    ```
    while (current != nullptr) {
        std::cout << "ID: " << current->data.id << std::endl;
        ...
        current = current->next;
    }
    ```
    If the linked list is empty, what will the output of `display` be?

24. **`src/LinkedList.cpp`**
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
    If two bugs have the same `id`, how does the sorting by id behave?

25. **`src/LinkedList.cpp`**
    ```
    while (getline(file, line)) {
        ...
        Bug bug;
        ...
        addBug(bug);
    }
    ```
    What could happen if the input file contains lines with missing fields when `loadFromFile` is called?

26. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        file << current->data.comments[i] << "|";
    }
    file << "||\n";
    ```
    What is the purpose of writing "||" at the end of each bug record in `saveToFile`?

27. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId) {

        BugNode* current = head;

        while (current != nullptr) {
            if (current->data.id == bugId) {
                return &current->data;
            }
            current = current->next;
        }

        return nullptr;
    }
    ```
    If you search for a bug id that matches more than one node, which one is returned and why?

28. **`src/LinkedList.cpp`**
    ```
    bug.commentCount = 0;

    while (getline(ss, comment, '|')) {
        if (comment.empty()) break;

        if (bug.commentCount < 10) {
            bug.comments[bug.commentCount++] = comment;
        }
    }
    ```
    What happens if the file contains more than 10 comments for a single bug?

29. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;
    ```
    Why is dynamic memory allocation used for each node in the linked list?

30. **`src/main.cpp`**
    ```
    Bug* found = list.searchBug(2);
    if (found) {
        std::cout << "\nFound Bug ID 2:\n";
        std::cout << found->briefDesc << std::endl;
    }
    ```
    If `searchBug` returns `nullptr`, what is the effect on the output in `main`?

31. **`src/LinkedList.cpp`**
    ```
    void LinkedList::sortByStatus() {
        if (!head) return;

        bool swapped;
        do {
            swapped = false;
            BugNode* current = head;

            while (current->next != nullptr) {
                if (current->data.status > current->next->data.status) {

                    Bug temp = current->data;
                    current->data = current->next->data;
                    current->next->data = temp;

                    swapped = true;
                }
                current = current->next;
            }
        }while (swapped);
    }
    ```
    How would the ordering of bugs change if all bugs had the same status value?

32. **`src/LinkedList.cpp`**
    ```
    void LinkedList::saveToFile(const std::string& filename) const {
        std::ofstream file(filename);

        BugNode* current = head;

        while (current != nullptr) {
            file << current->data.id << "|"
                 << current->data.date << "|"
                 << current->data.briefDesc << "|"
                 << current->data.detailedDesc << "|"
                 << current->data.status << "|"
                 << current->data.severity << "|";

            for (int i = 0; i < current->data.commentCount; i++) {
                file << current->data.comments[i] << "|";
            }
            file << "||\n";
            current = current->next;
        }

        file.close();
    };
    ```
    If `commentCount` is zero for a bug, what will be written for that bug's comments in the output file?

33. **`src/LinkedList.cpp`**
    ```
    BugNode* head = nullptr;
    ```
    What is the effect of initializing `head` to `nullptr` in the `LinkedList` class definition?

34. **`src/LinkedList.cpp`**
    ```
    std::ifstream file(filename);

    if (!file) {
        std::cout << "File not found.\n";
        return;
    }
    ```
    What is the behavior of `loadFromFile` if the file does not exist or cannot be opened?

35. **`src/LinkedList.h`**
    ```
    struct Bug {

        int id;
        std::string date;
        std::string  briefDesc;
        std::string  detailedDesc;
        std::string  status;
        std::string  severity;
        std::string  comments[10];
        int commentCount;
    };
    ```
    What is the maximum number of comments that can be stored for a bug and how is this enforced in the code?

36. **`src/LinkedList.cpp`**
    ```
    Bug b1 = {1, "2026-04-24", "Crash", "App crashes", "OPEN", "HIGH", "Needs fix"};
    ```
    How does the initialization of `Bug b1` assign its fields, considering the `comments` array?

37. **`src/main.cpp`**
    ```
    list.sortById();
    std::cout << "\nSorted by ID:\n";
    list.display();
    ```
    What is the effect on the displayed output if `sortById` is called after adding bugs in an arbitrary order?

38. **`src/main.cpp`**
    ```
    list.deleteBug(3);
    std::cout << "\nAfter Deletion:\n";
    list.display();
    ```
    After deleting the bug with id 3, what changes do you expect in the output of `display`?

39. **`src/main.cpp`**
    ```
    list.saveToFile("../output/bugFile.txt");
    ```
    What does this line in `main` accomplish, and where does the output go?

40. **`src/LinkedList.cpp`**
    ```
    BugNode* current = head;
    while (current != nullptr) {
        BugNode* next = current->next;
        delete current;
        current = next;
    }
    ```
    What could happen if you forgot to implement this destructor logic?

## Evaluation

_These questions require judging design decisions, tradeoffs, or rationale._

41. **`src/LinkedList.cpp`**
    ```
    void LinkedList::addBug(const Bug& bug) {
        BugNode* node = new BugNode;
        ...
        if (head == nullptr) {
            head = node;
            return;
        }
        ...
        current->next = node;
    }
    ```
    What are the tradeoffs of using a singly linked list for storing bugs versus an array or vector?

42. **`src/LinkedList.cpp`**
    ```
    Bug temp = current->data;
    current->data = current->next->data;
    current->next->data = temp;
    ```
    In sorting functions, why did you choose to swap the `Bug` objects instead of the actual node pointers, and what implications does this have?

43. **`src/LinkedList.cpp`**
    ```
    if (!head) return;
    ```
    Why is it important to check for an empty list before sorting or displaying, and what might happen if you do not?

44. **`src/LinkedList.h`**
    ```
    std::string  comments[10];
    int commentCount;
    ```
    Why did you limit the number of comments per bug to 10, and how might this constraint affect bug tracking in practice?

45. **`src/LinkedList.cpp`**
    ```
    void LinkedList::loadFromFile(const std::string& filename) {
        ...
        Bug bug;
        ...
        addBug(bug);
    }
    ```
    What design advantages or disadvantages are there to loading bugs from a file into a linked list structure?

46. **`src/LinkedList.cpp`**
    ```
    std::cout << "File not found.\n";
    ```
    What are the potential drawbacks of reporting file errors via `std::cout` versus using exceptions or error codes?

47. **`src/LinkedList.cpp`**
    ```
    for (int i = 0; i < current->data.commentCount; i++) {
        file << current->data.comments[i] << "|";
    }
    ```
    What considerations might you have about storing comments in a fixed-size array versus a dynamic container like `std::vector`?

48. **`src/LinkedList.cpp`**
    ```
    Bug* LinkedList::searchBug(int bugId)
    ```
    What are the risks or limitations of returning a pointer to a bug object from `searchBug`?

49. **`src/LinkedList.cpp`**
    ```
    BugNode* node = new BugNode;
    ```
    How does manual memory management in your linked list implementation compare to using smart pointers in modern C++?

50. **`src/LinkedList.cpp`**
    ```
    void LinkedList::display() const{
        ...
        std::cout << "ID: " << current->data.id << std::endl;
        ...
    }
    ```
    What implications does displaying bug information directly to `std::cout` have for modularity and reuse of your linked list class?

---

<sub>Generated by [grill-my-code](https://github.com/NSCC-ITC-Assessment/GrillMyCode) · gpt-4.1 via github-models · main</sub>