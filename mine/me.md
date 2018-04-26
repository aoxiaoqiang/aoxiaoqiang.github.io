# 个人收藏

```javascript
/**
 * 查找目标数组中最大值(最小值)的索引
 * @param Array arr 目标数组
 * @param String  type  只接受'min'和'max'或不传
 * @return Array
 */
function getArrayIndex(arr, type = 'min') {
  // 参数类型限制
  if (!(arr instanceof Array)) throw Error('参数类型错误!')
  if (type !== 'min' && type !== 'max') throw Error('参数错误!')
  
  let index = [0]
  return arr.reduce((accumulator, currentValue, currentIndex, array) => {
    // 选择一个对象基数作为最小值(最大值)
    const selectedVal = array[index[index.length - 1]]
    // 将当前值和基数做比较, 得到比较的结果。对结果进行判断处理
    const compareResult = (type === 'min' ? Math.min : Math.max)(currentValue, selectedVal)
    if (compareResult === currentValue && compareResult === selectedVal) {
      // 有相同的值, 添加当前索引值
      index.push(currentIndex)
    } else if (compareResult === currentValue) {
      // 当前值大于最小值(最大值), 更新最小值(最大值)索引
      index = [currentIndex]
    }
    return index
  })
}
```

```javascript
// 数组判断
// 1.
Array.isArray(obj)

// 2.
var isArray = Function.isArray || function(o) {
  return typeof o === 'object' && Object.prototype.toString.call(o) === '[object Array]'
}
```