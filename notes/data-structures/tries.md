# Tries

### YouTube Videos:

[Data Structures: Tries - HackerRank](https://www.youtube.com/watch?v=zIjfhVPRZCg)
[Trie Data Structure (EXPLAINED) - Fun With Code](https://www.youtube.com/watch?v=-urNrIAQnNo)
[Trie Data Structure - Beau teaches JavaScript - freeCodeCamp.org](https://www.youtube.com/watch?v=7XmS8McW_1U&index=9&list=PLWKjhJtqVAbkso-IbgiiP48n-O-JQA9PJ)

```JavaScript
class Node{
  constructor(){
    this.keys = new Map();
    this.end = false;
  }

  setEnd(){
    this.end = true;
  }

  isEnd(){
    return this.end;
  }
}

class Trie{
  constructor(){
    this.root = new Node();
  }

  print(){
    let arr = new Array();
    const search = (node, string) => {
      if (node.keys.size != 0){
        for (let l of node.keys.keys()){
          search(node.keys.get(l), string.concat(l));
        };
        if(node.isEnd()) {
          arr.push(string);
        };
      } else {
        string.length > 0 ? arr.push(string) : undefined;
        return;
      };
    };
    search(this.root, new String());
    return arr.length > 0 ? arr : null;
  };

  add(data, node = this.root){
    if(data.length === 0) {
      node.setEnd();
      return;
    };
    if(!node.keys.has(data[0])){
      node.keys.set(data[0], new Node());
      return this.add(data.substr(1), node.keys.get(data[0]));
    } else {
      return this.add(data.substr(1), node.keys.get(data[0]));
    };
  };

  isWord(word, node = this.root){
    while(word.length > 1) {
      if(!node.keys.has(word[0])){
         return false;
      } else {
        node = node.keys.get(word[0]);
        word = word.substr(1);
      };
    };
    return (node.keys.has(word) && node.keys.get(word).isEnd()) ? true : false
  };

};

let myTrie = new Trie();

myTrie = new Trie()
myTrie.add('first');
myTrie.add('second');
myTrie.add('secondary');
myTrie.add('third');
myTrie.add('fourth');
myTrie.add('four');
myTrie.add('fifth');
myTrie.add('sixth')
myTrie.add('silicon')
myTrie.add('send')
myTrie.add('see')
myTrie.add('sense')
myTrie.add('flamengo')
console.log(myTrie.isWord('zeus'));
console.log(myTrie.isWord('fla'));
console.log(myTrie.isWord('se'));
console.log(myTrie.isWord('flamengo'));
console.log(myTrie.isWord('send'));
console.log(myTrie.isWord('see'));
console.log(myTrie.print());


```
