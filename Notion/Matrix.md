- 通过获取account :

```Dart
LinphoneAccount *account =
      bctbx_list_nth_data(linphone_core_get_account_list(LC), idx);
```

- 通过 account 获取 index:

```Dart
int idx = (int)bctbx_list_index(linphone_core_get_account_list(LC), account);
```