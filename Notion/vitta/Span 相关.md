# 金额格式化

`https://github.com/terncommerce/span/blob/26d71140478d529c79e1f3c9c333230876ea47ed/span-web/src/CoreBundle/Twig/AppTwigExtension.php\#L21-L23`

```Plain
<td>{{ item.getTotalAmount()| money_format(item.getInitialCurrency()) }}</td>
```

# 格式化邮件发件人

```Plain
$data = json_decode($this->sender, true);
        if (empty($data) || is_string($data)){
            return $this->sender;
        }
        $senderStr = '';
        foreach ($data as $name => $email) {
            $senderStr .= $email . ' <' .$name.'>' ;
        }
        return $senderStr;
```

%0A%0A%23%23%20%E9%87%91%E9%A2%9D%E6%A0%BC%E5%BC%8F%E5%8C%96%0A%0A%60https%3A%2F%2Fgithub.com%2Fterncommerce%2Fspan%2Fblob%2F26d71140478d529c79e1f3c9c333230876ea47ed%2Fspan-web%2Fsrc%2FCoreBundle%2FTwig%2FAppTwigExtension.php%23L21-L23%60%0A%0A%60%60%60%0A%20%3Ctd%3E%7B%7B%20item.getTotalAmount()%7C%20money_format(item.getInitialCurrency())%20%7D%7D%3C%2Ftd%3E%0A%60%60%60%0A%0A%0A%23%23%20%E6%A0%BC%E5%BC%8F%E5%8C%96%E9%82%AE%E4%BB%B6%E5%8F%91%E4%BB%B6%E4%BA%BA%20%23%23%0A%60%60%60%0A%24data%20%3D%20json_decode(%24this-%3Esender%2C%20true)%3B%0A%20%20%20%20%20%20%20%20if%20(empty(%24data)%20%7C%7C%20is_string(%24data))%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20return%20%24this-%3Esender%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%24senderStr%20%3D%20''%3B%0A%20%20%20%20%20%20%20%20foreach%20(%24data%20as%20%24name%20%3D%3E%20%24email)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%24senderStr%20.%3D%20%24email%20.%20'%20%3C'%20.%24name.'%3E'%20%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20return%20%24senderStr%3B%0A%60%60%60%0A%0A