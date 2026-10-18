# Java Cheat Sheet (Compact)

Quick reference for common Java collection and graph operations.

---

## Arrays
- Initialize: `int[] a = {2,9,6,8,1,10};`
- Sort: `Arrays.sort(a);`
- Partial sort: `Arrays.sort(a, fromInclusive, toExclusive);`
- Binary search (after sort): `int idx = Arrays.binarySearch(a, key);`

---

## Lists
- Mutable: `List<Integer> list = new ArrayList<>(); list.add(1);`
- Fixed-size from values: `List<Integer> fixed = Arrays.asList(5,4,15);` (fixed-size)
- Create filled list: `List<Boolean> b = new ArrayList<>(Collections.nCopies(n, false));`
- Replace values: `Collections.fill(b, Boolean.TRUE);`

---

## Maps / Counters
- Count occurrences:
```java
Map<Integer,Integer> cnt = new HashMap<>();
for (Integer x : items) cnt.put(x, cnt.getOrDefault(x,0)+1);
```
- Iterate entries:
```java
for (Map.Entry<K,V> e : map.entrySet()) { K k = e.getKey(); V v = e.getValue(); }
```

---

## Sorting with Comparator
- Sort array or list with comparator:
```java
Arrays.sort(products, Comparator.comparingDouble(Product::price).reversed().thenComparing(Product::name));
// or
list.sort((a,b) -> Double.compare(b.price(), a.price()));
```

---

## Queues
- FIFO: `Queue<Integer> q = new LinkedList<>(); q.offer(x); q.poll();`
- Priority: `PriorityQueue<Integer> pq = new PriorityQueue<>();` (min-heap)
- Deque: `Deque<Integer> dq = new ArrayDeque<>(); dq.addFirst(x); dq.removeLast();`
- Blocking: `LinkedBlockingQueue` / `ArrayBlockingQueue` for producer-consumer

---

## DFS (recursive)
```java
void dfs(int u, List<List<Integer>> g, boolean[] vis, List<Integer> out){
  if (vis[u]) return; vis[u]=true; out.add(u);
  for (int v : g.get(u)) dfs(v,g,vis,out);
}
```

---

## BFS (iterative)
```java
List<Integer> bfs(int s, List<List<Integer>> g){
  boolean[] vis = new boolean[g.size()];
  List<Integer> res = new ArrayList<>();
  Deque<Integer> q = new ArrayDeque<>(); q.addLast(s); vis[s]=true;
  while(!q.isEmpty()){ int u=q.removeFirst(); res.add(u); for(int v:g.get(u)) if(!vis[v]){vis[v]=true; q.addLast(v);} }
  return res;
}
```

---

## Useful snippets
- Convert list -> array: `T[] arr = list.toArray(new T[0]);`
- Convert array -> list: `List<T> list = Arrays.asList(arr);`
- Create comparator by value: `Comparator<Map.Entry<K,Integer>> cmp = Map.Entry.comparingByValue();`
- Kth largest (min-heap of size k):
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
for (int x : arr) { pq.offer(x); if (pq.size()>k) pq.poll(); }
int kth = pq.peek();
```

---

Keep this file compact—tell me if you want it even shorter (one-liners) or expanded with explanations.
