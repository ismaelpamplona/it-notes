# Map data structure & ES6 map object

### YouTube Videos:

[Map data structure & ES6 map object - Beau teaches JavaScript freeCodeCamp.org](https://www.youtube.com/watch?v=_1BPrCHcjhs)

### My Map Class

```JavaScript
class MyMap {
  constructor (){
    this.collection = {};
    this.count = 0;
  }

  add(key, data){
    this.collection[key] = data;
    this.count++;
  }

  has(key){
    return (key in this.collection)
  }

  get(key){
    return this.has(key) ? this.collection[key] : null;
  }

  delete(key){
    if (this.has(key)){
      delete this.collection[key];
      this.count--;
    }
  }

  values(){
    let result = new Array();
    for(let key of Object.keys(this.collection)) {
      result.push(this.collection[key]);
    }
    return (result.length > 0) ? result : null;
  }

  clear(){
    this.collection = {};
    this.count = 0;
  }

  size(){
    return this.count;
  }

  show(){
    console.log(this.collection);
  }

}

const map1 = new MyMap();

map1.add("jan", 1);
map1.add("fev", 2);
map1.add("mar", 3);
map1.add("abr", 4);
map1.add("mai", 5);
map1.add("jun", 6);
map1.add("jul", 7);
map1.add("ago", 8);
map1.add("set", 9);
map1.add("out", 10);
map1.add("nov", 11);
map1.add("dez", 12);
map1.show()
console.log("size: " + map1.size());
console.log(map1.has("jan"));
console.log(map1.has("nonsense"));
console.log(map1.get("jun"))
map1.delete("jan");
map1.delete("fev");
map1.delete("mar");
map1.show();
console.log("size: " + map1.size());
console.log(map1.values());
map1.clear();
map1.show();
```

### ES6 Map

[MDN Web Docs - Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

```JavaScript
const map2 = new Map();

console.log(map2);
console.log(map2.has("flamengo"));
console.log(map2.entries());

let keyObj = {},
    keyFn = () => {};

map2.set("keyString", "string value key");
map2.set(keyObj, "obj value");
map2.set(keyFn, "fn value");
map2.set(NaN, "NaN 'value'");

console.log(map2.size); //size is a property and not a method

console.log(map2.get("keyString"));
console.log(map2.get(keyObj));
console.log(map2.get(keyFn));
console.log(map2.get(NaN));
```
