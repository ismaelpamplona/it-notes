# Heap

### YouTube Videos:

[Data Structures: Heaps - HackerRank](https://www.youtube.com/watch?v=t0Cq6tVNRBA)

[Heap Data Structure (max and min)- Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=dM_JHpfFITs&list=PLWKjhJtqVAbkso-IbgiiP48n-O-JQA9PJ&index=11&t=0s)

### Graph Visualization

[Min Heap Visualization - USFCA](https://www.cs.usfca.edu/~galles/visualization/Heap.html)

[Max Heap VIsualization - visualgo.net](https://visualgo.net/en/heap)

### Heap in JS

#### Min Heap

```JavaScript
// left child: i*2
// right child> i*2+1
// parent: i/2 (only the integer)

class MinHeap {
  constructor(){
    this.heap = new Array(null);
  }

  insert(num){
    this.heap.push(num);
    if(this.heap.length > 2){
      let i = this.heap.length-1;
      while(this.heap[i] < this.heap[Math.floor(i/2)]){
        if(i > 1){
          [this.heap[i], this.heap[Math.floor(i/2)]] = [this.heap[Math.floor(i/2)], this.heap[i]];
          i = Math.floor(i/2);
        } else {
          break;
        };
      };
    };
  };

  remove(){
    let smallest = this.heap[1];
    if(this.heap.length > 2){
      this.heap[1] = this.heap[this.heap.length-1]
      this.heap.splice(this.heap.length-1);
      if(this.heap.length === 3){
        if(this.heap[1] > this.heap[2]) {
          [this.heap[1], this.heap[2]] = [this.heap[2], this.heap[1]]
        };
        return smallest;
      };
      let i = 1;
      let left = i * 2;
      let right = i * 2 + 1;
      while(this.heap[i] >= this.heap[left] || this.heap[i] >= this.heap[right]){
        if(this.heap[left] < this.heap[right]){
          [this.heap[i], this.heap[left]] = [this.heap[left], this.heap[i]];
          i = i * 2;
        } else {
          [this.heap[i], this.heap[right]] = [this.heap[right], this.heap[i]];
          i = i * 2 + 1;
        }
        left = i * 2;
        right = i * 2 + 1;
        if ((this.heap[left] === undefined) || (this.heap[right] === undefined)){
          break;
        }
      }
    } else if (this.heap.length === 2){
      this.heap.splice(1,1);
    } else {
      return null;
    };
    return smallest;
  };

  sort(){
    let result = new Array(null);
    while(this.heap.length > 1){
      result.push(this.remove());
    }
    return result;
  };

};

const myMinHeap = new MinHeap();

console.log(myMinHeap)
console.log(myMinHeap.heap)
myMinHeap.insert(10);
myMinHeap.insert(9);
myMinHeap.insert(20);
myMinHeap.insert(60);
myMinHeap.insert(5);
myMinHeap.insert(30);
myMinHeap.insert(40);
myMinHeap.insert(50);
myMinHeap.insert(70);
myMinHeap.insert(5);
console.log(myMinHeap.heap);

myMinHeap.remove();
console.log(myMinHeap.heap);
console.log("sorted:", myMinHeap.sort());

```

#### Max Heap

```JavaScript
// left child: i*2
// right child> i*2+1
// parent: i/2 (only the integer)

class MaxHeap {
  constructor(){
    this.heap = new Array(null);
  }

  insert(num){
    this.heap.push(num);
    if(this.heap.length > 2){
      let i = this.heap.length-1;
      while(this.heap[i] > this.heap[Math.floor(i/2)]){
        if(i > 1){
          [this.heap[i], this.heap[Math.floor(i/2)]] = [this.heap[Math.floor(i/2)], this.heap[i]];
          i = Math.floor(i/2);
        } else {
          break;
        };
      };
    };
  };

  remove(){
    let highest = this.heap[1];
    if(this.heap.length > 2){
      this.heap[1] = this.heap[this.heap.length-1]
      this.heap.splice(this.heap.length-1);
      if(this.heap.length === 3){
        if(this.heap[1] < this.heap[2]) {
          [this.heap[1], this.heap[2]] = [this.heap[2], this.heap[1]]
        };
        return highest;
      };
      let i = 1;
      let left = i * 2;
      let right = i * 2 + 1;
      while(this.heap[i] <= this.heap[left] || this.heap[i] <= this.heap[right]){
        if(this.heap[left] > this.heap[right]){
          [this.heap[i], this.heap[left]] = [this.heap[left], this.heap[i]];
          i = i * 2;
        } else {
          [this.heap[i], this.heap[right]] = [this.heap[right], this.heap[i]];
          i = i * 2 + 1;
        }
        left = i * 2;
        right = i * 2 + 1;
        if ((this.heap[left] === undefined) || (this.heap[right] === undefined)){
          break;
        }
      }
    } else if (this.heap.length === 2){
      this.heap.splice(1,1);
    } else {
      return null;
    };
    return highest;
  };

  sort(){
    let result = new Array();
    while(this.heap.length > 1){
      result.unshift(this.remove());
    }
    result.unshift(null);
    return result;
  };

};

const myMaxHeap = new MaxHeap();

console.log(myMaxHeap)
console.log(myMaxHeap.heap)
myMaxHeap.insert(10);
myMaxHeap.insert(9);
myMaxHeap.insert(20);
myMaxHeap.insert(60);
myMaxHeap.insert(5);
myMaxHeap.insert(30);
myMaxHeap.insert(40);
myMaxHeap.insert(50);
myMaxHeap.insert(70);
console.log(myMaxHeap.heap);

myMaxHeap.remove();
console.log(myMaxHeap.heap);
console.log("sorted");
console.log(myMaxHeap.sort());
```
