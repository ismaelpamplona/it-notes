# Linked List

### YouTube Videos:

[Introduction to linked list - mycodeschool](https://www.youtube.com/watch?v=NobHlGUjV3g&t=6s)

[Linked List - Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=9YddVVsdG5A)

[Data Structures: Linked Lists - HackerRank](https://www.youtube.com/watch?v=njTh_OwMljA)

```javascript
// Linked List in JS

/* LinkedList */

function LinkedList() {
    var length = 0;
    var head = null;

    var Node = function(element) {
        this.element = element;
        this.next = null;
    };

    this.size = function() {
        return length;
    };

    this.head = function() {
        return head;
    };

    this.add = function(element) {
        var node = new Node(element);
        if (head === null) {
            head = node;
        } else {
            var currentNode = head;

            while (currentNode.next) {
                currentNode = currentNode.next;
            }

            currentNode.next = node;
        }

        length++;
    };

    this.remove = function(element) {
        var currentNode = head;
        var previousNode;
        if (currentNode.element === element) {
            head = currentNode.next;
        } else {
            while (currentNode.element !== element) {
                previousNode = currentNode;
                currentNode = currentNode.next;
            }

            previousNode.next = currentNode.next;
        }

        length--;
    };

    this.isEmpty = function() {
        return length === 0;
    };

    this.indexOf = function(element) {
        var currentNode = head;
        var index = -1;

        while (currentNode) {
            index++;
            if (currentNode.element === element) {
                return index;
            }
            currentNode = currentNode.next;
        }

        return -1;
    };

    this.elementAt = function(index) {
        var currentNode = head;
        var count = 0;
        while (count < index) {
            count++;
            currentNode = currentNode.next;
        }
        return currentNode.element;
    };

    this.addAt = function(index, element) {
        var node = new Node(element);

        var currentNode = head;
        var previousNode;
        var currentIndex = 0;

        if (index > length) {
            return false;
        }

        if (index === 0) {
            node.next = currentNode;
            head = node;
        } else {
            while (currentIndex < index) {
                currentIndex++;
                previousNode = currentNode;
                currentNode = currentNode.next;
            }
            node.next = currentNode;
            previousNode.next = node;
        }
        length++;
    };

    this.removeAt = function(index) {
        var currentNode = head;
        var previousNode;
        var currentIndex = 0;
        if (index < 0 || index >= length) {
            return null;
        }
        if (index === 0) {
            head = currentNode.next;
        } else {
            while (currentIndex < index) {
                currentIndex++;
                previousNode = currentNode;
                currentNode = currentNode.next;
            }
            previousNode.next = currentNode.next;
        }
        length--;
        return currentNode.element;
    };
}

var conga = new LinkedList();
conga.add("Kitten");
conga.add("Puppy");
conga.add("Dog");
conga.add("Cat");
conga.add("Fish");
console.log(conga.size());
console.log(conga.removeAt(3));
console.log(conga.elementAt(3));
console.log(conga.indexOf("Puppy"));
console.log(conga.size());
```

```Java
// Linked List in JAVA

/* LinkedList */

public class Node {
    Node next;
    int data;

    public Node(int data) {
        this.data = data;
    }
}

public class LinkedList {
    Node head;

    public void append(int data) {

        if (head == null) {
            head = new Node(data);
            return;
        }

        Node current = head;

        while (current.next != null) {
            current = current.next;
        }

        current.next = new Node(data);
    }

    public void prepend(int data) {
        Node newHead = new Node(data);
        newHead.next = head;
        head = newHead;

    }

    public void deleteValue(int data) {

        if (head == null) return;

        if (head.data == data) {
            head = read.next;
            return
        }

        Node current = head;

        while (current.next != null) {
            if (current.next.data == data) {
                current.next == current.next.next;
                return;
            }
            current = current.next;
        }
    }
}
```
