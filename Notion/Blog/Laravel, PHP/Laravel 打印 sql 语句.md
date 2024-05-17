  

```Plain
$sql = str_replace_array('?', $query->getBindings(), $query->toSql());
dd($sql);
```