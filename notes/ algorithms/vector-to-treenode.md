```Javascript
class TreeNode {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}

function from_vec_to_tn(vec, n) {
  let tn = null;
  if (vec.length === 0) {
    // base case
    return null;    
  } else if (n < vec.length) {
    // recursion
    tn = new TreeNode(vec[n]);
    tn.left = from_vec_to_tn(vec, 2 * n + 1);
    tn.right = from_vec_to_tn(vec, 2 * n + 2);
  }
  return tn;
}

const tnVec = [4, 2, 7, 1, 3, 6, 9,10,11,12];

console.log(from_vec_to_tn(tnVec, 0));
```