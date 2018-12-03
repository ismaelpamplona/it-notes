# Queues

### YouTube Videos

[]()

[Data Structures: Stacks and Queues - HackerRank](https://www.youtube.com/watch?v=wjI1WNcIntg)

[Queue | Data Structures Tutorial - Naresh i Technologies](https://www.youtube.com/watch?v=gnYM_G1ILm0)

[Queues & Priority Queues - Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=bK7I79hcm08&index=3&list=PLWKjhJtqVAbkso-IbgiiP48n-O-JQA9PJ)

```JavaScript
 // Queues in JS

 // Queues in JS

class Queue{
  constructor(){
    this.collection = new Array();
    this.head = null;
    this.tail = null;
  };

  add(data){ //enqueue
    this.collection.push(data);
    if(this.collection.length === 1){
      this.tail = data;
      this.head = data;
    } else {
      this.tail = data;
    };
  };

  remove(){ // dequeue
    this.collection.shift();
    if(this.collection.length > 0){
      this.head = this.collection[0];
    } else {
      this.head = null;
      this.tail = null;
    };
  };

  front(){
    return this.collection[0];
  };

  isEmpty(){
    return (this.collection.length === 0);
  };

  size(){
    return this.collection.length;
  };
};

const myQueue = new Queue();
console.log("________________ QUEUE _______________")
console.log(myQueue);
myQueue.add(1);
myQueue.add(2);
myQueue.add(3);
myQueue.add(4);
console.log(myQueue.front());
console.log(myQueue);
myQueue.remove();
myQueue.remove();
myQueue.add(1);
myQueue.add(2);
console.log(myQueue);
console.log(myQueue.front());

class PriorityQueue extends Queue{

    add(data){ // enqueue

      if (this.isEmpty()) {
        this.collection.push(data)
      } else {
        let added = false;
        for (let i = 0; i < this.collection.length; i++) {
          if (data[1] < this.collection[i][1]) {
            this.collection.splice(i, 0, data);
            added = true;
            break;
          };
        };
        if (!added) this.collection.push(data);
      };
    };

};

const pq = new PriorityQueue();
console.log("________________ PRIORITY QUEUE _______________")
pq.add(["John First P5", 5]);
pq.add(["John Second P3", 3]);
pq.add(["John Third P1", 1]);
pq.add(["John Fourth P1", 1]);
pq.add(["John Fifth P4", 4]);
pq.add(["John Sixth P2", 2]);
console.log(pq.front());
console.log(pq);
pq.remove();
pq.remove();
console.log(pq.front());
console.log(pq);


```
