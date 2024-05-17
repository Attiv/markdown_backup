使用`use`:

```Plain
$keyword    = $request->keyword;
        $waves      = \DB::table('user')->select('user.*')->leftJoin('tjy_device as d',
            function ($join) use ($keyword) {
                $join->on('tjy_wave_file.device_id', '=', 'd.id')->where('d.upload_path', 'like', '%'.$keyword.'%');
            })->simplePaginate($limit)->items();
```

%E4%BD%BF%E7%94%A8%60use%60%3A%0A%0A%60%60%60%0A%0A%20%24keyword%20%20%20%20%3D%20%24request-%3Ekeyword%3B%0A%20%20%20%20%20%20%20%20%24waves%20%20%20%20%20%20%3D%20%5CDB%3A%3Atable('user')-%3Eselect('user.*')-%3EleftJoin('tjy_device%20as%20d'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20function%20(%24join)%20use%20(%24keyword)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%24join-%3Eon('tjy_wave_file.device_id'%2C%20'%3D'%2C%20'd.id')-%3Ewhere('d.upload_path'%2C%20'like'%2C%20'%25'.%24keyword.'%25')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D)-%3EsimplePaginate(%24limit)-%3Eitems()%3B%0A%60%60%60