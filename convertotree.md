## 实现 convert 方法，把原始 list 转换成树形结构

```js
// 原始 list 如下
let list = [
  { id: 1, name: '部门A', parentId: 0 },
  { id: 2, name: '部门B', parentId: 0 },
  { id: 3, name: '部门C', parentId: 1 },
  { id: 4, name: '部门D', parentId: 1 },
  { id: 5, name: '部门E', parentId: 2 },
  { id: 6, name: '部门F', parentId: 3 },
  { id: 7, name: '部门G', parentId: 2 },
  { id: 8, name: '部门H', parentId: 4 }
];
const result = convert(list, ...);

// 转换后的结果如下
let result = [
  {
    id: 1,
    name: '部门A',
    parentId: 0,
    children: [{
      id: 3,
      name: '部门C',
      parentId: 1,
      children: [{
        id: 6,
        name: '部门F',
        parentId: 3
      }, {
        id: 16,
        name: '部门L',
        parentId: 3
      }]
    },
    {
      id: 4,
      name: '部门D',
      parentId: 1,
      children: [{
        id: 8,
        name: '部门H',
        parentId: 4
      }]
    }
    ]
  },
];
```

## 递归实现
```js
function convert(list, parentId = 0) {
  let tree = []
  list.forEach(function (item, index) {
    if (item.parentId === parentId) {
      let children = convert(list, item.id)
      if (children.length > 0) {
        item.children = children
      }
      tree.push(item)
    }
  })

  return tree
} 
```

## filter实现
```js
function convert(list) {
  return list.filter(function(item, index, arr){
    let children = arr.filter(function(sub){
      return sub.parentId === item.id
    })
    item.children = children
    return item.parentId === 0
  })
}
```
