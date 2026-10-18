# Java Cheat Sheet

## 1. Arrays

```java
int[] arr = {2, 9, 6, 8, 1, 10};
Arrays.sort(arr);               // full sort
Arrays.sort(arr, 1, 4);        // sort indexes 1..3

int key = 10;
int index = Arrays.binarySearch(arr, key); // works after sorting
```

---

## 2. List Initialization

```java
List<Integer> list = new ArrayList<>();
list.add(5);
list.add(4);
list.add(15);

// Alternative:
List<Integer> list2 = Arrays.asList(5, 4, 15); // fixed-size
```

```java
ArrayList<Boolean> flags = new ArrayList<>(Collections.nCopies(n, false));
Collections.fill(flags, Boolean.TRUE); // replace all values
```

---

## 3. Custom Comparator

```java
Comparator<Product> cmp = Comparator
    .comparingDouble(Product::price)
    .reversed()
    .thenComparing(Product::name);

Arrays.sort(products, cmp);
```

### Common comparator styles

- Method reference: `Comparator.comparingDouble(Product::price)`
- Lambda: `(p1, p2) -> Double.compare(p2.price(), p1.price())`
- Anonymous class: `new Comparator<Product>() { ... }`

---

## 4. Map Counter Pattern

```java
Map<Integer, Integer> counter = new HashMap<>();

for (Integer node : edgeNodesList) {
    counter.put(node, counter.getOrDefault(node, 0) + 1);
}
```

```java
for (Map.Entry<Integer, Integer> e : map.entrySet()) {
    if (e.getValue() % 2 != 0) {
        return false;
    }
}
```

---

## 5. Queue Types

```java
Queue<Integer> queue = new LinkedList<>();
queue.add(5);
Integer top = queue.poll();
```

### Queue basics

- Queue: FIFO (`LinkedList`)
- PriorityQueue: priority-based ordering
- Deque: add/remove from both ends (`ArrayDeque`, `LinkedList`)
- BlockingQueue: thread-safe producer/consumer queue

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(3);
pq.add(1);
pq.add(4);
pq.add(2);

while (!pq.isEmpty()) {
    System.out.println(pq.poll());   // 1, 2, 3, 4
}
```

---

## 6. DFS (Graph)

```java
static ArrayList<Integer> traverseList = new ArrayList<>();

static void dfsHelper(ArrayList<ArrayList<Integer>> graph, Integer node, ArrayList<Boolean> visited) {
    if (!visited.get(node)) {
        traverseList.add(node);
        visited.set(node, true);

        for (Integer neighbor : graph.get(node)) {
            dfsHelper(graph, neighbor, visited);
        }
    }
}
```

```java
ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

for (ArrayList<Integer> edge : edges) {
    int u = edge.get(0);
    int v = edge.get(1);
    graph.get(u).add(v);
    graph.get(v).add(u); // undirected graph
}
```

---

## 7. BFS (Graph)

```java
static ArrayList<Integer> bfs_traversal(Integer n, ArrayList<ArrayList<Integer>> edges) {
    ArrayList<ArrayList<Integer>> graph = new ArrayList<>(n);
    for (int i = 0; i < n; i++) {
        graph.add(i, new ArrayList<>());
    }

    for (ArrayList<Integer> edge : edges) {
        graph.get(edge.get(0)).add(edge.get(1));
        graph.get(edge.get(1)).add(edge.get(0));
    }

    ArrayList<Integer> visited = new ArrayList<>(Collections.nCopies(n, 0));
    ArrayList<Integer> unvisited = new ArrayList<>(Collections.nCopies(n, 1));
    ArrayList<Integer> result = new ArrayList<>();
    Deque<Integer> queue = new ArrayDeque<>();

    if (unvisited.get(0) == 1) {
        queue.addFirst(0);
        while (!queue.isEmpty()) {
            int node = queue.removeFirst();
            if (unvisited.get(node) == 1) {
                visited.set(node, 1);
                unvisited.set(node, 0);
            }

            for (int neighbor : graph.get(node)) {
                if (unvisited.get(neighbor) == 1) {
                    queue.addFirst(neighbor);
                    unvisited.set(neighbor, 0);
                }
            }
            result.add(node);
        }
    }

    return result;
}
```

---

## 8. Quick Notes

```java
// Convert array -> list
List<Integer> list = Arrays.asList(arr);

// Convert list -> array
Integer[] arr = list.toArray(new Integer[0]);

// Create list with repeated default values
List<Boolean> list = new ArrayList<>(Collections.nCopies(n, false));
```

---

## 9. Short Reminder

- `Arrays.sort()` sorts arrays in-place.
- `Collections.fill()` fills a list with a value.
- `PriorityQueue` works well for Kth largest problems.
- `HashMap` with `getOrDefault()` is useful for counters.
- `Deque` is best for BFS/queue-style operations.

