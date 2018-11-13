# Hashing, Hash Table

### YouTube Videos:

[Hasing in Data Structure List - saurabhschook](https://www.youtube.com/playlist?list=PLTZbNwgO5ebqw1v0ODk8cPLW9dQ99Te8f)

[Hash Tables - Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=F95z5Wxd9ks)

### HashTable in JS

```JavaScript
const hashFn = (str, max) => {

  var hash = 0;
  for (var i = 0; i < str.length; i++) {hash += str.charCodeAt(i)
    hash += str.charCodeAt(i);
  };
  return hash % max;

}

const HashTable = function(){

  let storage = [];
  const storageLimit = 37;

  this.print = function(){
    console.log(storage);
  };

  this.add = function(key, value){
    const index = hashFn(key, storageLimit);
    if (storage[index] === undefined){
      storage[index] = [
        [key, value]
      ];
    } else {
      var inserted = false;
      for (var i = 0; i < storage[index].length; i++){
        if (storage[index][i][0] === key){
          storage[index][i][1] = value;
          inserted = true;
        }
      }
      if (inserted == false){
        storage[index].push([key, value]);
      }
    }
  };

  this.remove = function(key){
    var index = hashFn(key, storageLimit);
    if (storage[index].length === 1 && storage[index][0][0] === key){
      delete storage[index];
    } else {
      for (var i = 0; i < storage[index].length; i++){
        if (storage[index][i][0] === key){
          delete storage[index][i]
        }
      }
    }
  };

  this.lookup = function(key){
    var index = hashFn(key, storageLimit);
    if (storage[index] === undefined){
      return undefined;
    } else {
      for (var i = 0; i < storage[index]; i++){
        if (storage[index][i][0] === key){
          return storage[index][i][1];
        }
      }
    }
  };

};

// testing the hash function

console.log(hashFn("Tim", 11));
console.log(hashFn("Tones", 11));
console.log(hashFn("Boo", 11));

// testing the Hash Table

const ht = new HashTable();

ht.add("Tim", "person");
ht.add('Pamplona', 'superhero');
ht.add('Boo', 'dog');
ht.add('Mingau', 'cat');
ht.add('Rex', 'dino');
ht.print();
```
