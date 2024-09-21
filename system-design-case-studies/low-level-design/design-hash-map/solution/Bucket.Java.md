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
