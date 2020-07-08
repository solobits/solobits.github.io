---
layout: post
title: Routing Using Get
---
Routing in Flutter is can be easy for small apps, but when you have quite a few pages you know that you need to manage them properly. Flutter gives you quite a few ways to do that, you might be doing it by using named routes or a package like auto_route. For this article we'll be using GET.

### GET, Router
GET which is not just a simple Routing solution but a Micro-Framework for Flutter. It has quite a lot that we can do with it like Dependency Management, State Management, Utils/Helpers and more. 

### Routing
We'll start by creating a new Flutter project. We'll use the default counter app and modify it using GET.

#### Importing Package
In pubspec.yaml import GET package. pubspec will then look something like this:

{% highlight js %}
environment:
  sdk: ">=2.7.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^0.1.3
  get: ^3.2.2

dev_dependencies:
  flutter_test:
    sdk: flutter
{% endhighlight %}

#### Base Setup
In your main.dart rename MaterialApp to GetMaterialApp. 

{% highlight js %}
import 'package:get/route_manager.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'Flutter Demo',
      initialRoute: routeOne,
      getPages: generateRoutes
    );
  }
}
{% endhighlight %}

#### Create a routes.dart file
Our ViewModel will have our business logic. Create getters and setters for the counter variable.

{% highlight js %}
import 'package:get/route_manager.dart';

import 'package:demo/pages/one_page.dart';
import 'package:demo/pages/two_page.dart';

const String routeOne = '/';
const String routeTwo = '/two';
mixin AppRoutes {
  final List<GetPage> generateRoutes = [
    GetPage(
        name: routeOne,
        page: () => const PageOne()),
        GetPage(
        name: routeTwo,
        page: () => const PageTwo()),
   
  ];
}

{% endhighlight %}


Now simply call Get.toNamed to navigate to a page or Get.offNamed to push to new page and replace current page.

{% highlight js %}
//Navigator.pushNamed 
FlatButton(onPressed: () => Get.toNamed(page))
//Navigator.pushReplacementNamed 
FlatButton(onPressed: () => Get.offNamed(page))
{% endhighlight %}

### Previous Articles on GET
<a href="https://medium.com/@solobits_nelson/state-management-using-get-e29d989ba97f" target="_blank">State Management using GET</a>

### Upcoming Articles
I'll be writing a list of Articles that will cover almost everything that we can do with GET namingly:

- Dependency Management
- Other Fun Helpers/Utilities (SnackBars, Dialog, BottomSheet etc)
- Architecture using GET

Hope it helps.


<section class="contact">
      <ul>
          <li class="github"><a href="https://github.com/solobits/" target="_blank"><i class="fa fa-github"></i></a></li>       
          <li class="linkedin"><a href="https://www.linkedin.com/in/solobits/" target="_blank"><i class="fa fa-linkedin" aria-hidden="true"></i></a></li>
          <li class="twitter"><a href="https://twitter.com/solobits_nelson" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>
          <li class="medium_platform"><a href="https://medium.com/@solobits_nelson" target="_blank"><i class="fa fa-medium" aria-hidden="true"></i></a></li>
      </ul>
</section>