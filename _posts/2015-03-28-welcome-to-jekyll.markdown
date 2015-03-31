---
layout: post
title:  "Your First Learning Algorithm: ZeroR!"
date:   2015-03-31 13:06:31
---
ZeroR is our least intelligent algorithm. It does not try to find any relations from the data. It just wants to be right as much as possible by settling on one, but only one result: it simply picks the most common label (i.e. majority class) in the dataset and returns this label for any future instance. 

For our rain predicting classifier for New York City, ZeroR algorithm will pick "NoEvent" as for New York weather data there are more "NoEvent" days than "Rain" days. In New York City, on average only one third of the days are rainy. ZeroR counts each category for our label ("Event column), and picks "Rain" as there are more "Rain" instances than "NoEvent" instances. 

ZeroR can be fun: imagine you are building a predictor for "whether a lottery ticket will win the lottery given all available data". ZeroR does not care about the "available data" part. It simply will say "NoWin" for any lottery ticket we put in. ZeroR will be right almost all the time, except that one time you win the lottery. :)

The trainer should look like:

{% highlight javascript linenos%}
function trainZeroR(instances) {
    var class_frequency = [];
    for (var i = 0; i < instances.length; i++) {
        var label = instances[i]["label"];
        if (class_frequency.hasOwnProperty(label)) {
            class_frequency[label]++;
        } else {
            class_frequency[label] = 1;
        }
    }
    var majority_label = "";
    var majority_label_freq = 0;
    for (var label in class_frequency) {
        if (class_frequency.hasOwnProperty(label)) {
            if (class_frequency[label] >= majority_label_freq) {
                majority_label = label;
                majority_label_freq = class_frequency[label];
            }
        }
    }
    return majority_label;
}
{% endhighlight %}

