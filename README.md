cssTest
=============

Vanilla Easing
-------------

```Javascript
function scrollIt(destination, duration, easing, callback) {

    var easings = {
        linear: function linear(t) {
            return t;
        },
        easeInQuad: function easeInQuad(t) {
            return t * t;
        },
        easeOutQuad: function easeOutQuad(t) {
            return t * (2 - t);
        },
        easeInOutQuad: function easeInOutQuad(t) {
            return t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t;
        },
        easeInCubic: function easeInCubic(t) {
            return t * t * t;
        },
        easeOutCubic: function easeOutCubic(t) {
            return --t * t * t + 1;
        },
        easeInOutCubic: function easeInOutCubic(t) {
            return t < 0.5 ? 4 * t * t * t : (t - 1) * (2 * t - 2) * (2 * t - 2) + 1;
        },
        easeInQuart: function easeInQuart(t) {
            return t * t * t * t;
        },
        easeOutQuart: function easeOutQuart(t) {
            return 1 - --t * t * t * t;
        },
        easeInOutQuart: function easeInOutQuart(t) {
            return t < 0.5 ? 8 * t * t * t * t : 1 - 8 * --t * t * t * t;
        },
        easeInQuint: function easeInQuint(t) {
            return t * t * t * t * t;
        },
        easeOutQuint: function easeOutQuint(t) {
            return 1 + --t * t * t * t * t;
        },
        easeInOutQuint: function easeInOutQuint(t) {
            return t < 0.5 ? 16 * t * t * t * t * t : 1 + 16 * --t * t * t * t * t;
        }
    };

    var start = window.pageYOffset;
    var startTime = 'now' in window.performance ? performance.now() : new Date().getTime();

    var documentHeight = Math.max(document.body.scrollHeight, document.body.offsetHeight, document.documentElement.clientHeight, document.documentElement.scrollHeight, document.documentElement.offsetHeight);
    var windowHeight = window.innerHeight || document.documentElement.clientHeight || document.getElementsByTagName('body')[0].clientHeight;
    var destinationOffset = typeof destination === 'number' ? destination : destination.offsetTop;
    var destinationOffsetToScroll = Math.round(documentHeight - destinationOffset < windowHeight ? documentHeight - windowHeight : destinationOffset);

    if ('requestAnimationFrame' in window === false) {
        window.scroll(0, destinationOffsetToScroll);
        if (callback) {
            callback();
        }
        return;
    }

    function scroll() {
        var now = 'now' in window.performance ? performance.now() : new Date().getTime();
        var time = Math.min(1, (now - startTime) / duration);
        var timeFunction = easings[easing](time);
        window.scroll(0, Math.ceil(timeFunction * (destinationOffsetToScroll - start) + start));

        if (window.pageYOffset === destinationOffsetToScroll) {
            if (callback) {
                callback();
            }
            return;
        }

        requestAnimationFrame(scroll);
    }

    scroll();
}
```







사용할때
-------------


```Javascript
for (var scrollEl of document.getElementsByClassName('scroll')){
    scrollEl.addEventListener('click', function () {
        var target = this.getAttribute('data-scroll-target');
        scrollIt(
            document.getElementsByClassName(target)[0],
            300,
            'easeOutQuad',
            () => console.log(`Just finished scrolling to ${window.pageYOffset}px`)
        );
    })
}
```