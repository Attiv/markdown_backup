`$query = Role::where('name', 'like', "%$keyword%")->orWhereHas('permissions', function ($q) use ($keyword) { $q->where('name', 'like', "%$keyword%"); });`

```Plain
   $query = Role::where('name', 'like', "%$keyword%")->orWhereHas('permissions', function ($q) use ($keyword) {
            $q->where('name', 'like', "%$keyword%");
        });
        
```