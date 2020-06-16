---
layout: post
title: State Management Using Get
---
The following article assumes you are already aware of State Management Basics. We'll be using a package called GET for this article.

If you want to learn about the basics follow the official Flutter documentation which explains State Management very good: https://flutter.dev/docs/development/data-and-backend/state-mgmt

### GET, Juiced State Manager
We do have multiple options to achieve this namingly InheritedWidgets, ScopedModel, Provider, Bloc, MobX etc. But we'll be using GET which is not just a simple State Management solution but a Micro-Framework for Flutter. It has quite a lot that we can do with it like Dependency Management, Router, Utils/Helpers and more. 

So basically GET is on Steroids. We'll start by talking about how it can help us manage our state.

### State Management
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
  get:

dev_dependencies:
  flutter_test:
    sdk: flutter
{% endhighlight %}

#### Base Setup
In your main.dart rename MaterialApp to GetMaterialApp. 

{% highlight js %}
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}
{% endhighlight %}

#### Create your ViewModel/Controller
Our ViewModel will have our business logic. Create getters and setters for the counter variable.

{% highlight js %}
class CounterViewmodel extends GetController {
  int _counter = 0;

  int get counter => _counter;
  set counter(int val) {
    _counter = val;
    update();
  }
}
{% endhighlight %}


Wrap the widget you want to update in GetBuilder

{% highlight js %}
GetBuilder<CounterViewmodel>( //It's something like a consumer that we use in Provider
              init: CounterViewmodel(),
              builder: (_) => Text(
                '${_.counter}',
                style: Theme.of(context).textTheme.headline4,
              ),
            ),
            {% endhighlight %}

To trigger an increment we'll do something like this

{% highlight js %}
floatingActionButton: FloatingActionButton(
        onPressed: () {
          final _viewmodel = Get.find<CounterViewmodel>(); //Just like we use Provider.of for Provider

          _viewmodel.counter = _viewmodel.counter + 1;
        },
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
      {% endhighlight %}

Run your app and Voila!. That's all you need.

<img src="https://solobits.github.io/public/gifs/2020_06_16-statemgmt-get.gif"/>

### Upcoming Articles
I'll be writing a list of Articles that will cover almost everything that we can do with GET namingly:

- Dependency Management
- Router
- Other Fun Helpers/Utilities (SnackBars, Dialog, BottomSheet etc)
- Architecture using GET

Hope it helps.

<a href="https://github.com/solobits/get_sm" target="_blank">Source Code</a> 

<section class="contact">
      <ul>
          <li class="github"><a href="https://github.com/solobits/" target="_blank"><i class="fa fa-github"></i></a></li>       
          <li class="linkedin"><a href="https://www.linkedin.com/in/solobits/" target="_blank"><i class="fa fa-linkedin" aria-hidden="true"></i></a></li>
          <li class="twitter"><a href="https://twitter.com/solobits_nelson" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>
          <li class="medium_platform"><a href="https://medium.com/@solobits_nelson" target="_blank"><i class="fa fa-medium" aria-hidden="true"></i></a></li>
      </ul>
</section>