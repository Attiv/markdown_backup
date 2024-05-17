```JavaScript
/**
 * 类似padStart，超出部分截取，只保留length 长的字符串，不足部分用 char补足
 * @param content 要截取字符串
 * @param length 截取长度
 * @param char 不足补充的字符串
 * @returns {string}
 */
export function stringFixedStart (content, length, char = ' ') {
  let target
  if (content.length > length) {
    target = content.substring(0, length - 3) + '...'
  } else {
    target = _.padStart(content, length, ' ')
  }
  return target
}

/**
 * 类似padEnd，超出部分截取，只保留length 长的字符串，不足部分用 char补足
 * @param content 要截取字符串
 * @param length 截取长度
 * @param char 不足补充的字符串
 * @returns {string}
 */
export function stringFixedEnd (content, length, char = ' ') {
  let target
  if (content.length > length) {
    target = content.substring(0, length - 3) + '...'
  } else {
    target = _.padEnd(content, length, char)
  }
  return target
}
```