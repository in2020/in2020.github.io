---
layout: post
title:  "iOS safari momentum scrolling bug"
date:   2019-02-13 22:28:21 +0900
tags: [vue]
categories: ios
---

ios safari 에서 -webkit-overflow-scrolling:touch와 position:fixed를 같이 사용할 경우 스크롤 버그가 있다.

재현 방법 
- 아래 코드 상태에서 스크롤을 최상단에 두고 터치후 아래로 드래그
- 아래 코드 상태에서 스크롤을 최하단에 두고 터치후 위로 드래그

위와 같이 수행 할 경우 스크롤이 2~3초 안됨(가속 효과가 끝날때 까지)

{% highlight html %}
<body style="position:fixed;left:0;top:0;height:100%;width:100%;background-color:red">
  <div style="position:fixed;left:0;top:0;height:100%;width:100%;background-color:green;-webkit-overflow-scrolling:touch;overflow-y:auto">
    <p style="height:3000px;width:100%;background-color:blue">
    </p>
  </div>
</body>
{% endhighlight %}

내가 찾은 해결 방법

참조 : [reference-stackoverflow]

{% highlight javascript %}
var lastY = 0; // Needed in order to determine direction of scroll.
$(".scroller").on('touchstart', function(event) {
    lastY = event.touches[0].clientY;
});

$('.scroller').on('touchmove', function(event) {
    var top = event.touches[0].clientY;

    // Determine scroll position and direction.
    var scrollTop = $(event.currentTarget).scrollTop();
    var direction = (lastY - top) < 0 ? "up" : "down";

    // FIX IT!
    if (scrollTop == 0 && direction == "up") {
      // Prevent scrolling up when already at top as this introduces a freeze.
      event.preventDefault();
    } else if (scrollTop >= (event.currentTarget.scrollHeight - event.currentTarget.outerHeight()) && direction == "down") {
      // Prevent scrolling down when already at bottom as this also introduces a freeze.
      event.preventDefault();
    }

    lastY = top;
});
{% endhighlight %}

[reference-stackoverflow]: https://stackoverflow.com/questions/39692337/div-scrolling-freezes-sometimes-if-i-use-webkit-overflow-scrolling
