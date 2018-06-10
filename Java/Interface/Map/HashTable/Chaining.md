# Chaining 방법
* 저장할 위치가 동일한 값들을 LinkedList에 저장합니다.
![Chaining](img/Chaining.png)

* Chaining 구현
```
public class Chaining {
    
    static class Node {
        int value;
        Node next;
        
        public Node(int value, Node next) {
            this.value = value;
            this.next = next;
        }
        
        static Node remove(Node node, int value) {
            if (node == null) return null;
            if (node.value == value) return node.next;
            node.next = remove(node.next, value);
            return node;
        }
        
        static boolean contains(Node node, int value) {
            if (node == null) return false;
            if (node.value == value) return true;
            return contains(node.next, value);
        }
    }
    
    static class HashTable {
        static final int SIZE = 37;
        Node[] a;
        
        public HashTable() {
            a = new Node[SIZE];
        }
        
        public void add(int value) throws Exception {
            int index = value % SIZE;
            a[index] = new Node(value, a[index]);
        }
        
        public void remove(int value) {
            int index = value % SIZE;
            a[index] = Node.remove(a[index], value);
        }
        
        public boolean contains(int value) {
            int index = value % SIZE;
            return Node.contains(a[index], value);
        }
    }
    
    public static void main(String[] args) throws Exception {
        int maxValue = 200, maxCount = 10;
        int[] data = { 4, 13, 144, 7, 9, 11, 44, 115, 107, 196 };
        HashTable hashTable = new HashTable();
        
        for (int i = 0; i < data.length; ++i) {
            hashTable.add(data[i]);
        }
        
        hashTable.remove(11);
        hashTable.remove(44);
        
        for (int i = 1; i <= maxValue; ++i) {
            if (hashTable.contains(i)) {
                System.out.println(i);
            }
        }
    }
}
```