大小写和shift 设置

符号总结

# 大小写和shift 设置

```Swift
# 中西文切換鍵的默認設置寫在 default.yaml 裏面 
 # 以下的 default.custom.yaml 在全局範圍重定義該組快速鍵 
 # 
 # 可用的按鍵有 Caps_Lock, Shift_L, Shift_R, Control_L, control_R 
 # Mac 系統上的鼠鬚管不能區分左、右，因此只有對 Shift_L, Control_L 的設定起作用 
 # 
 # 已輸入編碼時按切換鍵，可以進一步設定輸入法中西文切換的形式。 
 # 可選的臨時切換策略有三： 
 # inline_ascii 在輸入法的臨時西文編輯區內輸入字母、數字、符號、空格等，回車上屏後自動復位到中文 
 # commit_text 已輸入的候選文字上屏並切換至西文輸入模式 
 # commit_code 已輸入的編碼字符上屏並切換至西文輸入模式 
 # 設爲 noop，屏蔽該切換鍵 
 # 
 # 如果要把 Caps Lock 設爲只改變字母的大小寫而不做中西文切換，可將 Caps_Lock 對應的切換方式設爲 noop 
 # 如果要以 Caps Lock 切換到西文模式，默認輸出小寫字母，請置 ascii_composer/good_old_caps_lock: false 
 # 如果要以 Caps Lock 切換到西文模式，默認輸出大寫字母，請使用以下設置： 
   patch: 
 ascii_composer/good_old_caps_lock: true 
 ascii_composer/switch_key: 
 Caps_Lock: commit_code 
 Shift_L: noop 
 Shift_R: noop 
 Control_L: commit_code 
 Control_R: commit_code
```

  

# 符号总结

|   |   |
|---|---|
|键位|说明|
|BackSpace|退格|
|Tab|水平定位符|
|Linefeed|换行|
|Clear|清除|
|Return|回车|
|Pause|暫停|
|Sys_Req|印屏|
|Escape|退出|
|Delete|刪除|
|Home|原位|
|Left|左箭头|
|Up|上箭头|
|Right|右箭头|
|Down|下箭头|
|Prior、Page_Up|上翻|
|Next、Page_Down|下翻|
|End|末位|
|Begin|始位|
|Shift_L|左Shift|
|Shift_R|右Shift|
|Control_L|左Ctrl|
|Control_R|右Ctrl|
|Meta_L|左Meta|
|Meta_R|右Meta|
|Alt_L|左Alt|
|Alt_R|右Alt|
|Super_L|左Super|
|Super_R|右Super|
|Hyper_L|左Hyper|
|Hyper_R|右Hyper|
|Caps_Lock|大写锁|
|Shift_Lock|上档锁|
|Scroll_Lock|滚动锁|
|Num_Lock|小键盘锁|
|Select|选定|
|Print|列印|
|Execute|执行|
|Insert|插入|
|Undo|还原|
|Redo|重做|
|Menu|菜单|
|Find|搜索|
|Cancel|取消|
|Help|帮助|
|Break|中断|
|space|空格|
|exclam|!|
|quotedbl|"|
|numbersign|#|
|dollar|$|
|percent|%|
|ampersand|&|
|apostrophe|'|
|parenleft|(|
|parenright|)|
|asterisk|*|
|plus|+|
|comma|,|
|minus|-|
|period|.|
|slash|/|
|colon|:|
|semicolon|;|
|less|<|
|equal|=|
|greater|>|
|question|?|
|at|@|
|bracketleft|[|
|backslash||
|bracketright|]|
|asciicircum|^|
|underscore|_|
|grave|`|
|braceleft|{|
|bar||
|braceright|}|
|asciitilde|~|
|KP_Space|小键盘空格|
|KP_Tab|小键盘水平定位符|
|KP_Enter|小键盘回车|
|KP_Delete|小键盘删除|
|KP_Home|小键盘原位|
|KP_Left|小键盘左箭头|
|KP_Up|小键盘上箭头|
|KP_Right|小键盘右箭头|
|KP_Down|小键盘下箭头|
|KP_Prior、KP_Page_Up|小键盘上翻|
|KP_Next、KP_Page_Down|小键盘下翻|
|KP_End|小键盘末位|
|KP_Begin|小键盘始位|
|KP_Insert|小键盘插入|
|KP_Equal|小键盘等于|
|KP_Multiply|小键盘乘号|
|KP_Add|小键盘加号|
|KP_Subtract|小键盘减号|
|KP_Divide|小键盘除号|
|KP_Decimal|小键盘小数点|
|KP_0|小键盘0|
|KP_1|小键盘1|
|KP_2|小键盘2|
|KP_3|小键盘3|
|KP_4|小键盘4|
|KP_5|小键盘5|
|KP_6|小键盘6|
|KP_7|小键盘7|
|KP_8|小键盘8|
|KP_9|小键盘9|