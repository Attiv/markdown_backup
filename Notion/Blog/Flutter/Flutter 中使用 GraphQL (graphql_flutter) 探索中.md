## 安装

这里使用 [graphql_flutter 5.1.0](https://pub.dev/packages/graphql_flutter)`flutter pub add graphql_flutter`

> 版本变化挺大，所以这里用最新的 5.1.0

## 使用

在 Flutter 中使用 [GraphQL](https://graphql.org/) 跟使用 Restful API 区别很大，graphql_flutter 是用 Widget 的方式，也可以使用 [flutter_hooks](https://pub.dev/packages/flutter_hooks) 的方式，这里介绍常规 Widget Query 和 Mutation 方式

1. 创建 Client

```Plain
import 'package:graphql_flutter/graphql_flutter.dart';
import 'package:flutter/material.dart';

ValueNotifier<GraphQLClient> clientFor({
  @required String uri,
  String subscriptionUri,
}) {
  Link httpLink = HttpLink(
    uri,
    // TODO: add headers here
    defaultHeaders: {
      'date': DateTime.now().toString(),
      'content-type': 'application/json; charset=utf-8',
    },
  );
  if (subscriptionUri != null) {
    final WebSocketLink websocketLink = WebSocketLink(
      subscriptionUri,
    );
    httpLink = Link.split((request) => request.isSubscription, websocketLink, httpLink);
  }

  final AuthLink authLink = AuthLink(
    getToken: () => 'Bearer ${your_token}',
  );
  final Link link = authLink.concat(httpLink);
  return ValueNotifier<GraphQLClient>(
    GraphQLClient(
      cache: GraphQLCache(store: HiveStore()),
      link: link,
    ),
  );
}
```

1. 创建 Provider

```Plain
import 'package:flutter/material.dart';
import 'package:graphql_flutter/graphql_flutter.dart';
import 'package:xxxx/graphql_provider.dart';

/// Wraps the root application with the `graphql_flutter` client.
/// We use the cache for all state management.
class ClientProvider extends StatelessWidget {
  ClientProvider({
    @required this.child,
    @required String uri,
    String subscriptionUri,
  }) : client = clientFor(
          uri: uri,
          subscriptionUri: subscriptionUri,
        );

  final Widget child;
  final ValueNotifier<GraphQLClient> client;

  @override
  Widget build(BuildContext context) {
    return GraphQLProvider(
      client: client,
      child: child,
    );
  }
}
```

1. 在 `main.dart` 里 `runApp(App());` 前加入`await initHiveForFlutter(); // 缓存用`
2. 在 `app.dart` 里

```Plain
return Builder(
      builder: (BuildContext context) {
        return ClientProvider(
          child: buildApp(context),
          uri: serverUrl,
        );
      },
    )
```

1. **请求**  
    这里和平常使用的 Restful API 有很大的区别， 在需要发送请求的地方(比如 Button) 上  
    

```Plain
Mutation(
                            options: MutationOptions(
                              document: gql(r'''
                  mutation ($phoneNumber: String!) {
                  sendVerificationCode(phoneNumber: $phoneNumber) {
                    ... on ErrorResult {
                      errorCode
                      message
                    }
                    ... on Other {
                    success
                    status
                   result
                  }
                    __name
                  }
                }
        '''),
                              onCompleted: (dynamic resultData) {

                                print(resultData);

                              },
                            ),
                            builder: (
                              RunMutation runMutation,
                              QueryResult result,
                            ) {

                              if (result.hasException) {
                                print(result.exception);

                              }
                              return Button(
                                  onPressed: _canClick != true
                                      ? null
                                      : () {
                                          runMutation({'phoneNumber': '123456789'});
                                        },
                                  borderRadius: BorderRadius.circular(8),
                                  width: 182,
                                  height: 40,
                                  text: 'Button,
                                  fontSize: 15,
                                  weight: FontWeight.w600,
                                  textColor: Colors.white,
                                  color: style.primaryColor);
                            },
                          ),
```

> onCompleted 里返回的是接口正常返回的信息  
> runMutation 就是发送请求, runMutation({参数: value})document 是需要发送的 GraphQLQuery 的和 Mutations 类似，把 Mutations 改成 Query  

## 结尾

基础的简单使用就到这里了，如果有更好的方法或者深入的用法，欢迎分享。