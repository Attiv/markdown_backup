```Plain
dyld: Library not loaded: /usr/local/opt/jpeg/lib/libjpeg.8.dylib
  Referenced from: /usr/local/bin/php
  Reason: image not found
[1]    24171 abort      php -v
```

解决方法： `brew switch libjpeg 8d`