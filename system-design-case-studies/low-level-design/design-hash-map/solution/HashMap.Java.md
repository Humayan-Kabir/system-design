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
