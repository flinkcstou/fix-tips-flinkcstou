Offline-first tools for web developers
======

A quick list of tools for building HTML/CSS/JS apps that work well offline. Ping me at [@nolanlawson](https://twitter.com/nolanlawson) if I missed anything!

Hybrid app development
-------

Tools for bundling your HTML/CSS/JS into a native app.

* [Cordova](https://cordova.apache.org/)/[PhoneGap](http://phonegap.com/)
* [Node-Webkit](https://github.com/rogerwang/node-webkit)
* [Atom Shell](https://github.com/atom/atom-shell)
* [Chrome apps](https://developer.chrome.com/apps/about_apps)
* [WinJS](https://github.com/winjs/winjs)

UI Frameworks
---------

Frameworks designed to work well on mobile devices. A good pairing with the above build tools.

* [Ionic Framework](http://ionicframework.com/)
* [Famo.us](http://famo.us/)
* [JQuery Mobile](http://jquerymobile.com/)
* [Sencha Touch](http://www.sencha.com/products/touch)
* [Kendo UI](http://www.telerik.com/kendo-ui)

Databases and wrappers
---------

Tools to help you use LocalStorage, Web SQL, and IndexedDB in the browser.

* [PouchDB](http://pouchdb.com/)
* [LocalForage](https://github.com/mozilla/localforage)
* [YDN-DB](http://dev.yathit.com/ydn-db/index.html)
* [Dexie](https://github.com/dfahlander/Dexie.js)
* [IndexedDBShim](https://github.com/axemclion/IndexedDBShim)
* [Lawnchair](http://brian.io/lawnchair/)

#### Level* community

One API, many backends. Mostly server-side, but some client-side libraries too:

* [level.js](https://github.com/maxogden/level.js) (IndexedDB)
* [IndexedUp](https://github.com/ricardobeat/indexedup) (IndexedDB)
* [localstorage-down](https://github.com/No9/localstorage-down) (LocalStorage)
* [SQLdown](https://github.com/calvinmetcalf/SQLdown) (SQL databases, including Web SQL) 
* [MemDOWN](https://github.com/rvagg/memdown) (in-memory)
* [More](https://github.com/rvagg/node-levelup/wiki/Modules)
 
All-in-one frameworks
------

[Hood.ie](http://hood.ie/) kind of stands alone in this regard. There's nothing quite like it!

Web APIs
-----

Web APIs that help your app work well offline. Some new and immature technology, but still useful.

* [Application Cache](http://www.html5rocks.com/en/tutorials/appcache/beginner/)
  * Also [this article](http://alistapart.com/article/application-cache-is-a-douchebag) is a bit caustic, but still contains good tips (warning: language).
* [Service Workers](http://www.w3.org/TR/service-workers/)
  * Very green &ndash; only supported in Chrome currently. Also, does not work with IndexedDB on Firefox and IE. Still exciting!
  * [Great talk introducing it](https://www.youtube.com/watch?v=_yy0CDLnhMA) 