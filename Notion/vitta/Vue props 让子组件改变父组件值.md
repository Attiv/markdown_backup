```Plain
<child-component :props.sync='要改变的值'>
```

子组件更新数值：

```Plain
this.$emit('update:data', 要更改的数值)
```

%0A%60%60%60%0A%3Cchild-component%20%3Aprops.sync%3D'%E8%A6%81%E6%94%B9%E5%8F%98%E7%9A%84%E5%80%BC'%3E%0A%60%60%60%0A%E5%AD%90%E7%BB%84%E4%BB%B6%E6%9B%B4%E6%96%B0%E6%95%B0%E5%80%BC%EF%BC%9A%0A%60%60%60%0Athis.%24emit('update%3Adata'%2C%20%E8%A6%81%E6%9B%B4%E6%94%B9%E7%9A%84%E6%95%B0%E5%80%BC)%0A%60%60%60