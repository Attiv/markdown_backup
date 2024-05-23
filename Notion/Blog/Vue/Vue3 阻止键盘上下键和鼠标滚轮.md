```
export const preventUpDown = (event: any, isInt = false) => {
  // 阻止按键默认行为
  if (event.key === 'ArrowUp' || event.key === 'ArrowDown') {
    event.preventDefault()
  }
  // 阻止滚轮默认行为
  if (event.type === 'wheel') {
    event.preventDefault()
  }

  if (isInt) {
    const invalidChars = ['e', 'E', '+', '-', '.']
    if (invalidChars.includes(event.key)) {
      event.preventDefault()
    }
  }
}
```

在UI l里这么写：
```
<el-input
        class="no-number"
        v-model="input"
        @keydown="preventUpDown"
        @wheel="preventUpDown"
      />
```

## 去除 type="number" 的上下框
```
// main.scss 里
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

input[type='number'] {
  -moz-appearance: textfield;
}
```