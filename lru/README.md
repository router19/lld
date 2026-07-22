Things we need 
- A node with key, value, prev and next pointers 
- A map with key to node pairs 
- A DLL with most recent at head and LRU at tail. 
- get() : if the key is present in map, move the node to head and return value. else return -1 
- put(key,value) : if the key is present in map, update value and move to head. else, if cache is full, remove the LRU node and add the new node to head. 
```java

class LRUCache {
class Node {
  K Key;
  V Value;
  Node next;
  Node prev;

  public Node(K key, V value) {
    this.key = key;
    this.value = value;
  }
  public Node(V value)  {
    this.value = value;
  }
}

  private Map<K,Node> cache;
  int capacity; 
  Node head;
  Node tail;


  public LRuCache(int capacity){
    this.capacity = capacity;
    cache = new HashMap<>();
    head = new Node(null,null);
    tail = new Node(null,null);
    head.next = tail;
    tail.prev = head; 
  }  

  public V get(K key) {
    if(cache.containsKey(key)){
      Node node = cache.get(key);
      moveToHead(node);
      return node.value;
    }
    return null;
  }

  public void put(K key,V value) {
    if(cache.containsKey(key)){
      Node node = cache.get(key);
      node.value = value;
      moveToHead(node);
    }else{
      if(cache.size() == capacity){
        Node node = tail.prev;
        removeNode(node);
        cache.remove(node.key);
      }
      Node node = new Node(key,value);
      addNode(node);
      cache.put(key,node);
    }
    
  }

  private void removeNode(Node node){
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  private void addNodeToHead(Node node){
    node.next = head.next;
    node.prev = head;
    head.next.prev = node;
    head.next = node;
  }

  private void moveToHead(Node node){
    removeNode(node);
    addNodeToHead(node);
  }  
}  
```