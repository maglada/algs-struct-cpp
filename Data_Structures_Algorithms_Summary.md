
# Data Structures and Algorithm Analysis in C++ (Конспект Алгоритмів)

---

## 1. Стек (Stack)
### Опис
Стек — це структура даних типу LIFO (Last In, First Out). Використовується для управління викликами функцій, перевірки збалансованості дужок тощо.

### Реалізація
#### Однозв'язний список
```cpp
struct Node {
    int data;
    Node* next;
};

class Stack {
    Node* top;
public:
    Stack() : top(nullptr) {}
    void push(int x) {
        Node* temp = new Node();
        temp->data = x;
        temp->next = top;
        top = temp;
    }
    void pop() {
        if (top != nullptr) {
            Node* temp = top;
            top = top->next;
            delete temp;
        }
    }
    int peek() {
        return (top != nullptr) ? top->data : -1; // -1 if stack is empty
    }
};
```

### Часова складність
- **Операції push та pop**: O(1)

---

## 2. Черга (Queue)
### Опис
Черга — це структура даних типу FIFO (First In, First Out). Використовується для управління потоками завдань, BFS у графах тощо.

### Реалізація
#### На основі масиву
```cpp
class Queue {
    int* arr;
    int front, rear, capacity;
public:
    Queue(int size) : front(0), rear(0), capacity(size) {
        arr = new int[size];
    }
    void enqueue(int x) {
        if (rear < capacity) arr[rear++] = x;
    }
    void dequeue() {
        if (front < rear) front++;
    }
    int peek() {
        return (front < rear) ? arr[front] : -1;
    }
};
```

### Часова складність
- **Вставка та видалення**: O(1)

---

## 3. Сортування (Sorting)
### Опис
Розділ містить опис класичних алгоритмів сортування.

#### 3.1 Сортування вставками (Insertion Sort)
```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### Часова складність
- **Найгірший випадок**: O(n^2)
- **Найкращий випадок**: O(n)

---

## 4. Графи (Graphs)
### Опис
Алгоритми роботи з графами, включаючи пошук у глибину (DFS), ширину (BFS), та алгоритми найкоротших шляхів.

#### 4.1 Пошук у ширину (BFS)
```cpp
void BFS(int start, vector<vector<int>>& adjList) {
    vector<bool> visited(adjList.size(), false);
    queue<int> q;
    visited[start] = true;
    q.push(start);
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";
        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

### Часова складність
- **BFS**: O(V + E), де V — кількість вершин, E — кількість ребер.

---
