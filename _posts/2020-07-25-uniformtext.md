---
layout: post
title: Uniform Text Sizes Across the App in Flutter
---
If you're new to Flutter or a Pro we know how much of the Text Widget we use... Some large in size, some small, some bold and the list goes on. Having uniform text sizes and attributes across the app is very important for the UI/UX. So I just decided to share a small tip for new devs on who can they do it.

### Steps
We're are simply going to create a Text widget in our project that we can then call across our app.

#### Create a new file called text.dart

{% highlight js %}
import 'package:flutter/material.dart';

//Enum for different text types, you can add more
enum TextType { sm, body, subtitle, title, xl }

const double fontSize = 14.0;
// Inspired by VelocityX
// Scale factors as found in VelocityX package
const double scaleFactorBase = 1;
const double scaleFactorLg = 1.120;
const double scaleFactorXl = 1.25;
const double scaleFactorXl2 = 1.5;
const double scaleFactorXl3 = 1.875;
const double scaleFactorXl4 = 2.25;
const double scaleFactorXl5 = 3;
const double scaleFactorXl6 = 4;

class AppText extends StatelessWidget {
  //some common attributes. You can change as needed
  final String text;
  final TextType type;
  final Color color;
  final TextAlign align;
  final double scaleFactor;
  final FontWeight weight;
  final bool underline;

  const AppText(
      {@required this.text,
      @required this.type,
      this.color,
      this.align,
      this.scaleFactor,
      this.weight,
      this.underline = false,
      Key key})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Text(text,
        style: TextStyle(
            color: color ?? _colorByTextType(type),
            fontSize: fontSize,
            fontWeight: weight ?? FontWeight.normal,
            decoration: underline ? TextDecoration.underline : null),
        textScaleFactor: scaleFactor ?? _scaleFactorByTextType(type),
        textAlign: align ?? TextAlign.start);
  }

  Color _colorByTextType(TextType type) {
    Color _color = Colors.black87;

    switch (type) {
      case TextType.sm:
        _color = Colors.white;
        break;
      case TextType.body:
        _color = Colors.black;
        break;
      case TextType.subtitle:
        _color = Colors.red;
        break;
      case TextType.title:
        _color = Colors.green;
        break;
      case TextType.xl:
        _color = Colors.blue;
        break;
      default:
        break;
    }

    return _color;
  }

  double _scaleFactorByTextType(TextType type) {
    double _factor = scaleFactorBase;

    switch (type) {
      case TextType.sm:
        _factor = scaleFactorBase;
        break;
      case TextType.body:
        _factor = scaleFactorLg;
        break;
      case TextType.subtitle:
        _factor = scaleFactorXl;
        break;
      case TextType.title:
        _factor = scaleFactorXl2;
        break;
      case TextType.xl:
        _factor = scaleFactorXl3;
        break;
      default:
        break;
    }

    return _factor;
  }
}

{% endhighlight %}

#### Usage

Now in any file of you project simply call AppText widget. e.g:

{% highlight js %}
 AppText(text: title,
         type: TextType.title,
         color: Colors.pink,
         weight: FontWeight.w600,
        align: TextAlign.center)

{% endhighlight %}



Hope it helps.

<section class="contact">
      <ul>
          <li class="github"><a href="https://github.com/solobits/" target="_blank"><i class="fa fa-github"></i></a></li>       
          <li class="linkedin"><a href="https://www.linkedin.com/in/solobits/" target="_blank"><i class="fa fa-linkedin" aria-hidden="true"></i></a></li>
          <li class="twitter"><a href="https://twitter.com/solobits_nelson" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>
          <li class="medium_platform"><a href="https://medium.com/@solobits_nelson" target="_blank"><i class="fa fa-medium" aria-hidden="true"></i></a></li>
      </ul>
</section>