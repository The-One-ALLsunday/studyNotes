# 经典算法

## 基础算法

### 二分法

```javascript
const arr = [1,2,3,4,5,6,7,8];

const binarySearchFn = (arr, value) => {
  let low = 0;
  let high = arr.length - 1;
  while(low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (value === arr[mid]) {
      return mid;
    } else if (value < arr[mid]) {
      high = mid - 1;
    } else {
      low = mid + 1;
    };
  };
  return -1;
};
```

### 冒泡排序

```javascript
const arr = [1,3,4,6,7,2,9,8];

for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length - i -1; j++) {
  	if (arr[j] > arr[j+1]) {
      let temp = arr[j+1];
      arr[j+1] = arr[j];
      arr[j] = temp;
    };
  };
};
```



