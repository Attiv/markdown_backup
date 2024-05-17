It seems like CORS error is well-known issue in the web field. But I tried flutter web for the first time ever and I faced critical error.

The code below worked well in app version when it was running on iOS device, but when i tested the same code on Chrome with web debugging from beta channel, it encountered CORS error.

Other stackoverflow answers explained how to solve the CORS issue with serverside files of their projects. But I have totally no idea what is server thing and how to deal with their answers. The error message from Chrome console was below

[Access to XMLHttpRequest at ‘https://kapi.kakao.com/v1/payment/ready’ from origin ‘http://localhost:52700’ has been blocked by CORS policy: Response to preflight request doesn’t pass access control check: No’Access-Control-Allow-Origin’ header is present on the requested resource.]

So, what i want to do is to solve above ‘Access-Control-Allow-Origin header’ issue ONLY WITH DART CODE! Code below is what i’ve tried to solve these issues only with my main.dart.

```Plain
onPressed: () async {
      var res =
          await http.post('https://kapi.kakao.com/v1/payment/ready', encoding: Encoding.getByName('utf8'), headers: {
        'Authorization': 'KakaoAK $_ADMIN_KEY',
        HttpHeaders.authorizationHeader: 'KakaoAK $_ADMIN_KEY',
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "POST, GET, OPTIONS, PUT, DELETE, HEAD",
      }, body: {
        'cid': 'TC0ONETIME',
        'partner_order_id': 'partner_order_id',
        'partner_user_id': 'partner_user_id',
        'item_name': 'cool_beer',
        'quantity': '1',
        'total_amount': '22222',
        'vat_amount': '2222',
        'tax_free_amount': '0',
        'approval_url': '$_URL/kakaopayment',
        'fail_url': '$_URL/kakaopayment',
        'cancel_url': '$_URL/kakaopayment'
      });
      Map<String, dynamic> result = json.decode(res.body);
      print(result);
    },
```

Even though i actually had the header `"Access-Control-Allow-Origin": "*"` which most other answers recommended, the Chrome console printed same error message. Weird thing is that the same code made successful request in mobileApp version. So I think this is only problem with flutter WEB VERSION.

Hope somebody can figure it out and suggest only-dart code to resolve the issue in my main.dart!! Thank you for reading [:

[![](https://lh3.googleusercontent.com/a-/AAuE7mBm2zpGXASAWq7g-MMicwPLreIdiYwIHYCIGxHc=k-s64)](https://lh3.googleusercontent.com/a-/AAuE7mBm2zpGXASAWq7g-MMicwPLreIdiYwIHYCIGxHc=k-s64)

joe

1- Go to `flutter\bin\cache` and remove a file named: `flutter_tools.stamp`

2- Go to `flutter\packages\flutter_tools\lib\src\web` and open the file `chrome.dart`.

3- Find `'--disable-extensions'`

4- Add `'--disable-web-security'`

[![](https://i.stack.imgur.com/lCW0u.jpg?s=64&g=1)](https://i.stack.imgur.com/lCW0u.jpg?s=64&g=1)

Osman Tuzcu

Using [Osman Tuzcu](https://stackoverflow.com/users/10757031/osman-tuzcu)’s answer, I created [flutter_cors](https://pub.dev/packages/flutter_cors) to make the process easier.

[![](https://i.stack.imgur.com/fTt3G.jpg?s=64&g=1)](https://i.stack.imgur.com/fTt3G.jpg?s=64&g=1)

Rexios

run/compile your Flutter web project using web-renderer. This should solve the issue both locally and remotely:

```Plain
flutter run -d chrome --web-renderer html
flutter build web --web-renderer html
```

[![](https://i.stack.imgur.com/qBxce.png?s=64&g=1)](https://i.stack.imgur.com/qBxce.png?s=64&g=1)

Praharsh Bhatt

I think disabling web security as suggested will make you jump over the current error for now but when you go for production or testing on other devices the problem will persist because it is just a workaround, the correct solution is from the server side to allow CORS from the requesting domain and allow the needed methods, and credentials if needed.

[![](https://lh3.googleusercontent.com/-HhhwcRMr_zI/AAAAAAAAAAI/AAAAAAAAAHo/ElV4-iDOsXk/photo.jpg?sz=64)](https://lh3.googleusercontent.com/-HhhwcRMr_zI/AAAAAAAAAAI/AAAAAAAAAHo/ElV4-iDOsXk/photo.jpg?sz=64)

Tommy

Server side engine like node js or django is really needed to work with flutter web with bunch of external apis. Actually there’s high possibility of same CORS error when we try to use internal api because of the CORS mechanism related to port number difference.

There are bunch of steps and answers from SO contributors that recommend to use chrome extensions to avoid CORS errors, but that is actually not cool for users. All the users should download the browser extensions to use the single website from us, which wouldn’t be there if we used true server engines.

CORS is from browser as far as i know, so our flutter ios and android apps with same api code don’t give those CORS errors. First time i encountered this error with flutter web, i believed i can deal with CORS in my app code lines. But that is actually not healthy way for users and long term dev plans.

Hope all flutter web newbies understand that web is quite a wild field for us. Even though i’m also newbie here, i highly recommend all the flutter web devs from 1.22.n stable to learn server side engines like node js. It is worth try.

And if u came so far down to this line of my self-answer, here’s a simple guide for flutter web with node js. Flutter web is on stable channel but all those necessary infra are not fully ready for newbies like me. So be careful when you first dive into web field, and hope you re-check all the conditions and requirements to find out if you really need web version of your flutter app, and also if you really need to do this work with flutter. And my answer was yes lol

[https://blog.logrocket.com/flutter-web-app-node-js/](https://blog.logrocket.com/flutter-web-app-node-js/)

[![](https://graph.facebook.com/314591235618040/picture?type=large)](https://graph.facebook.com/314591235618040/picture?type=large)

tsitixe

If you run a Spring Boot server, add “@CrossOrigin” to your Controller or to your service method.

```Plain
@CrossOrigin
@PostMapping(path="/upload")
public @ResponseBody ResponseEntity<Void> upload(@RequestBody Object object) {
    // ...
}
```

I know the question explicitly asked for a solution “with dart code” only, but I was not able to fix the exception with dart code (for example by changing the header).

[![](https://lh3.googleusercontent.com/a-/AAuE7mBm2zpGXASAWq7g-MMicwPLreIdiYwIHYCIGxHc=k-s64)](https://lh3.googleusercontent.com/a-/AAuE7mBm2zpGXASAWq7g-MMicwPLreIdiYwIHYCIGxHc=k-s64)

Bobin

This official solution worked for me on Chrome only ([Source](https://docs.flutter.dev/development/tools/web-renderers)). But I had to run it first every time.

```Plain
flutter run -d chrome --web-renderer html
```

And disabling web security also worked ([Source](https://stackoverflow.com/a/66879350/15526921)). But the browsers will show a warning banner.

But In case you are running on a different browser than Chrome (_e.g. Edge_) and you want to keep ‘web security’ enabled. **You can change the default web renderer in settings in VS Code**

> File ==> Preferences ==> Settings ==> Enter ‘Flutter Web’ in the Search Bar ==> Set the default web renderer to html

[![](https://www.gravatar.com/avatar/3a0df5aac80330aa2ba38ff90a555485?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/3a0df5aac80330aa2ba38ff90a555485?s=64&d=identicon&r=PG&f=1)

Ali Ali El-Dabaa

This is a CORS (cross-origin resource sharing) issue and you do not have to delete/modify anything. You just have to enable the CORS request from your server-side and it will work fine.

In my case, I have created a server with node.js and express.js, so I just added this middleware function that will run for every request.

```Plain
app.use(function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Methods", "GET,PUT,PATCH,POST,DELETE");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});
```

And BOOOOM! I received the data.

You just have to look at the settings to enable CORS for your server.

[![](https://www.gravatar.com/avatar/c93c1fc6a412cbbc00707fed508f57f2?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/c93c1fc6a412cbbc00707fed508f57f2?s=64&d=identicon&r=PG&f=1)

Nimantha

[https://docs.flutter.dev/development/platform-integration/web-images](https://docs.flutter.dev/development/platform-integration/web-images)

```Plain
flutter run -d chrome --web-renderer html
flutter build web --web-renderer html
```

[![](https://www.gravatar.com/avatar/f9aab67045fa891d26b9a14a215a512a?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/f9aab67045fa891d26b9a14a215a512a?s=64&d=identicon&r=PG&f=1)

Ali Murtaza

The disabling web security approaches work well in development, but probably not so well in production. An approach that worked for me in production dart code involves avoiding the pre-flight CORS check entirely by keeping the web request simple. In my case this meant changing the request header to contain:

```Plain
'Content-Type': 'text/plain'
```

Even though I’m actually sending json, setting it to text/plain avoids the pre-flight CORS check. The lambda function I’m calling didn’t support pre-flight OPTIONS requests.

Here’s some info on other ways to [keep a request simple](https://medium.com/@praveen.beatle/avoiding-pre-flight-options-calls-on-cors-requests-baba9692c21a) and avoid a pre-flight request

[![](https://lh6.googleusercontent.com/-Ab_j9gaxe6c/AAAAAAAAAAI/AAAAAAAAAAo/YJLwPWlOv4o/photo.jpg?sz=64)](https://lh6.googleusercontent.com/-Ab_j9gaxe6c/AAAAAAAAAAI/AAAAAAAAAAo/YJLwPWlOv4o/photo.jpg?sz=64)

justcodepy

After hours of testing, the following works perfectly for me.

Add the following to the PHP file:

```Plain
header('Access-Control-Allow-Origin: *');
header('Access-Control-Allow-Methods: GET, POST');
header("Access-Control-Allow-Headers: X-Requested-With");
```

This allow the correct connection with the HTTP GET POST with no issue from flutter for me.

I discovered this in the following discussion:

[XMLHttpRequest error Flutter](https://github.com/flutter/flutter/issues/57421)

[![](https://www.gravatar.com/avatar/cbddb462c2438298c4b62fe3ca02a392?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/cbddb462c2438298c4b62fe3ca02a392?s=64&d=identicon&r=PG&f=1)

Tim R

I think you may not doing this in right way. The cors headers should be added in HTTP response header while you added them in you reuqest header obviously.

for more information check out the documentation [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#what_requests_use_cors](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#what_requests_use_cors)

[![](https://www.gravatar.com/avatar/?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/?s=64&d=identicon&r=PG&f=1)

CNK

The below solution is great if you are only communicating with a local NodeJS server.

1. [Install NodeJS](https://nodejs.org/en/download/)
2. Create a basic NodeJS express project
    - Create a folder to put you NodeJS project in
        - ex: `C:\node_project\`
        - in PowerShell run: `npm init` in the folder
            - fill in your desired values
            - `entry point:` must be `app.js` for this example to work
        - in PowerShell run: `npm install express` in the folder
        - create a `app.js` file in the folder

```Plain
// init express
const express = require("express");
const app = express();

// set the path to the web build folder
app.use(express.static("C:/Users/your_username/path_to_flutter_app/build/web"));

const PORT = process.env.PORT || 8080;
app.listen(PORT, () => {
    console.log(`Server listening on port ${PORT}...`);
});
```

- The value `"C:/Users/your_username/path_to_flutter_app/build/web"` must be changed to the web build folder in your flutter app.
- The app can be accessed through your browser once the app is built, the node server is running, and the browser is at the correct address
    - Build the app
        - open PowerShell and navigate to the flutter project’s root ex: `C:/Users/your_username/path_to_flutter_app/`
        - run `flutter build web`
    - turn on the node server
        - open PowerShell and navigate to the NodeJS server folder ex: `C:\node_project\`
        - run: `node app.js`
    - Open in your browser
        - Enter `http://localhost:8080/` into the browser

_**Note that everytime you change your flutter app’s dart code you will need to re-run**_ `_**flutter build web**_`

[![](https://www.gravatar.com/avatar/1855e720a305dc9aba4fa70a20f1576d?s=64&d=identicon&r=PG&f=1)](https://www.gravatar.com/avatar/1855e720a305dc9aba4fa70a20f1576d?s=64&d=identicon&r=PG&f=1)

ostcollect

### Update

I recommend to use [Rexios’s answer](https://stackoverflow.com/a/70660912/410996). His package makes it very convenient to modify the Flutter source code.

---

## Alternative solution for MacOS & Android Studio (without modifying Flutter source)

We use a similar approach as Osman Tuzcu. Instead of modifying the Flutter source code, we add the `--disable-web-security` argument in a shell script and just forward all other arguments that were set by Flutter. It might look overly complicated but it takes just a minute and there is no need to repeat it for every Flutter version.

### 1. Run this in your terminal

```Plain
echo '#!/bin/zsh
# See also https://stackoverflow.com/a/31150244/410996
trap "trap - SIGTERM && kill -- -$$" SIGINT SIGTERM EXIT
set -e ; /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --test-type --disable-web-security "$@" ; set +e &
PID=$!
wait $PID
trap - SIGINT SIGTERM EXIT
wait $PID
' > ~/chrome_launcher

chmod 755 ~/chrome_launcher
```

This adds a `chrome_launcher` script to your user folder and marks it executable.

### 2. Add this line to your `.zshrc` (or `.bashrc` etc.):

```Plain
export CHROME_EXECUTABLE=~/chrome_launcher
```

### 3. Restart Android Studio

If a simple restart does not work, use **Invalidate Caches / Restart** in Android Studio to force loading of changes.

### Notes

The script also adds the `--test-type` flag to suppress the ugly warning about the disabled security features. Be aware that this option might also suppress other error messages! The `CHROME_EXECUTABLE` takes only the path to an executable file it is not possible to set arguments there. Without trapping exit signals and killing the process group, the Google Chrome instance was not killed when you hit the **Stop Button** in Android Studio. > 本文由简悦 SimpRead 转码