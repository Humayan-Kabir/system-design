# Design HashMap
---

![[design-hashmap.webp]]

## Requirement
* get(key)
* put(key)
* remove(key)
all the operation should be supported with O(1) complexity.

---

```java
// Node class for holding key value pair
package design.hashmap;  
  
public class Node<K, V> {  
    private K key;  
    private V value;  
  
    public Node(K key, V value) {  
        this.key = key;  
        this.value = value;  
    }  
  
    public K getKey() {  
        return key;  
    }  
  
    public void setKey(K key) {  
        this.key = key;  
    }  
  
    public V getValue() {  
        return value;  
    }  
  
    public void setValue(V value) {  
        this.value = value;  
    }  
}
```

---

```java
// Bucket class for handling collusion
package design.hashmap;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class Bucket<K, V> {  
    private final List<Node<K, V>> nodes;  
  
    public Bucket() {  
        nodes = new ArrayList<>();  
    }  
  
    public Node<K, V> get(K key) {  
        for (Node<K, V> node : nodes) {  
            if (node.getKey().equals(key)) {  
                return node;  
            }  
        }  
        return null;  
    }  
  
    public Node<K, V> put(K key, V value) {  
        Node<K, V> existingNode = get(key);  
        if (existingNode != null) {  
            existingNode.setValue(value);  
            return existingNode;  
        }  
        nodes.add(new Node<>(key, value));  
        return null;  
    }  
  
    public Node<K, V> remove(K key) {  
        Node<K, V> existingNode = get(key);  
        if (existingNode != null) {  
            nodes.remove(existingNode);  
        }  
        return existingNode;  
    }  
  
    private Node<K, V> findNode(K key) {  
        for (Node<K, V> node : nodes) {  
            if (node.getKey().equals(key)) {  
                return node;  
            }  
        }  
        return null;  
    }  
}
```

---

```java
// Custom HashMap class
package design.hashmap;  
  
import java.util.ArrayList;  
import java.util.List;  
  
public class CustomHashMap<K, V> {  
    private final List<Bucket<K, V>> buckets;  
    private final int capacity;  
    private int size;  
  
    public CustomHashMap(int capacity) {  
        this.buckets = new ArrayList<>();  
        this.capacity = capacity;  
        this.size = 0;  
        for (int i = 0; i < capacity; i++) {  
            buckets.add(new Bucket<>());  
        }  
    }  
  
    public V get(K key) {  
        int hashCode = getBucketIndex(key);  
        Node<K, V> node = buckets.get(hashCode).get(key);  
        if (node != null) {  
            return node.getValue();  
        }  
        return null;  
    }  
  
    public V put(K key, V value) {  
        int hashCode = getBucketIndex(key);  
        Node<K, V> node = buckets.get(hashCode).put(key, value);  
        if (node != null) {  
            return node.getValue();  
        }  
        size++;  
        return null;  
    }  
  
    public V remove(K key) {  
        int hashCode = getBucketIndex(key);  
        Node<K, V> node = buckets.get(hashCode).remove(key);  
        if (node != null) {  
            size--;  
            return node.getValue();  
        }  
        return null;  
    }  
  
    public int size() {  
        return size;  
    }  
  
    public boolean isEmpty() {  
        return size == 0;  
    }  
  
    private int getBucketIndex(K key) {  
        return Math.abs(key.hashCode()) % capacity;  
    }  
}
```

