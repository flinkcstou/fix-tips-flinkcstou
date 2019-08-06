- На iOS устройствах числовые значения подчёркиваются синим. Эта проблема возникает из-за того, что iOS устройства по умолчанию считают все числа похожие на телефонные номера - телефонными номерами. Решается добавлением `<meta name="format-detection" content="telephone=no" />`
Тоже самое касается адреса: `<meta name="format-detection" content="address=no" />`


- Пользователь может уменьшать и увеличивать приложение. Решается добавляением тега `<meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width, height=device-height, target-densitydpi=device-dpi" />`


- Ссылки нажимаются с задержкой (примерно 300ms). Решается подпиской на событие touchstart и принудительной инициализацией события click после него. Если проблема всё равно возникает - ничего не поделать, надо облегчать dom.
Как вариант - можно использовать библиотеку, посоветанную [@adubovsky](https://gist.github.com/adubovsky) ниже в комментариях: https://gist.github.com/SerafimArts/de9900f9977780de355d#gistcomment-1430896

- В android появляется синяя обводка вокруг ссылок с характерным звуком. Решение:

```css
* {
    -webkit-tap-highlight-color: rgba(255, 255, 255, 0);
    -webkit-focus-ring-color: rgba(255, 255, 255, 0);
    outline: none;
    user-select: none;
    -webkit-text-size-adjust: none;
}
input, textarea {
  -webkit-user-select: auto !important;
}
```

```js
document.addEventListener("touchstart", function () {}, true);
```
иногда придётся добавить, бывают проблемы в вёрстке
```css
background: rgba(0, 0, 0, 0);
```

- В android устройствах возникает полная перерисовка webview. Решение: Запретить смену ориентации - надо прописать в activity манифеста `android:configChanges="keyboardHidden|orientation|screenSize"`

- После сворачивания/разворачивания приложения могут возникнуть ситуации дублирования webview. Решается прописыванием 
```
android:clearTaskOnLaunch="true"
android:noHistory="true"
android:launchMode="singleTask"
```
в activity в манифесте

- Есть проблемы со строкой состояния - она видна у андроид и ios. Для скрытия оной требуется прописать:
`android:theme="@android:style/Theme.NoTitleBar.Fullscreen"` в application манифеста андройда и заменить 

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    // Do any additional setup after loading the view from its nib.
}
```
на 
```
- (void)viewDidLoad
{
    [super viewDidLoad];
    // Do any additional setup after loading the view from its nib.

    if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 7) {
        CGRect viewBounds = [self.webView bounds];
        viewBounds.origin.y = 20;
        viewBounds.size.height = viewBounds.size.height - 20;
        self.webView.frame = viewBounds;
    }
    self.view.backgroundColor = [UIColor blackColor];
}

-(UIStatusBarStyle)preferredStatusBarStyle{
    return UIStatusBarStyleLightContent;
}
```
внутри файла `/platforms/ios/имя_приложения/Classes/MainViewController.m`

- Все события проходят сквозь весь лайаут по z-index. Невозможно заблокировать экран каким-нибудь всплывающим окном - при нажатии на ссылку, которая находится под каким-нибудь элементом - она всё равно нажмётся.
Решение: Через раз помогает добавление `preventDefault`, `stopPropagation` и `return false` на onclick внутрь элемента c наибольшим z-index, но работает не всегда.

- На самсунге (android) все тач события могут останавливать отрисовку и тормозить. Решение: смириться, ничего не поделаешь

- Appliction Error. Ошибка выглядит как 
```bash
Appliction Error
The connection to the server was unsuccessful (file:///ansdorid_assets/www/index.html)
```
Решение: переименовать файл index.html в app.html, создать новый index.html и вставить туда:
```
<script>
    window.location='./app.html';
</script>
```

- В iOS не работает масштабирование шрифта. Решение: css `-webkit-text-size-adjust: auto;`

- Могут возникнуть ошибки, когда элемент рисуется в одном месте, а реальное физическое положение в совершенно другом (актуально для samsung). Решение: Избавиться от `margin` и `padding`, пробовать выравнивать элементы иначе

- Как можно меньше использовать SVG - это замедляет работу приложения, особенно на девайсах с высокой плотностью пикселей.

- Как можно меньше использовать box-shadow, gradient, border-radius и rgba - это сильно снижает производительность приложения

- Не располагать input и textarea элементы внизу страницы - поведение клавиатуры зачастую не предсказуемо.

- Не использовать position fixed элементы. Во время скролла страницы они зачастую западают, а при отображении клаиватуры могут повиснуть на середине экрана (очень часто на iOS устройствах). Решается подёргиванием лайаута на 1 пиксель влево-вправо - fixed элемент сбрасывается до своей изначальной позции.

- Не используйте длинные списки и\или длинный контент  - на iOS устройствах при скролле все изображения в списках размываются и периодически можно получить чёрный экран.

- Старайтесь использовать GPU - фикс вида `translate3d(0,0,0)` - зачастую позволяет ускорить отрисовку.

- В phonegap приложении не называйте каталоги словом bin - в phonegap версии 3.0+ (вроде) приложение может не собраться.

- Нельзя называть каталоги словами, содержащие зарезервированные слова (даже частично). Например `classasdasd/` стоит переименовть в `klassasdasd/`

- css background подгружается только тогда, когда элемент показывается на экране, img src, подгружается сразу.
- Есть багфикс для вебкита - он позволяет снизить оверхед CPU в некоторых приложениях:
```
-webkit-animation: bugfix infinite 1s;
@-webkit-keyframes bugfix
{
    from { padding: 0; }
    to { padding: 0; }
}
```

- Используйте свойство zoom - оно позволяет подогнать любое приложение под треубемое разрешение по горизонтали

- Включение скроллбара: `-webkit-overflow-scrolling: touch;`

- Не использовать spritesheet - на устройствах с высоким ppi иконки могут поехать и выглядывать куски других.

- Не использовать gif-анимации - помимо того, что они физически тормозят, дополнительно они тормозят всю систему

- Чем меньше css и проще dom, тем быстрее приложение - это не касается JS, он летает.




Касательно проблемы с задержкой 300мс, мы у себя на проекте используем FastClick библиотечку (https://github.com/ftlabs/fastclick)
 


**Ahead-of-Time compiling**


- Building applications to run on IOS & Android? Don't forget to implement Ahead-of-Time (AoT) compiling with the addition of the --prod flag:

`ionic cordova build ios --prod`

`ionic cordova build android --release --prod`

Ahead-of-Time compiling improves performance by compiling templates at build time NOT runtime. This leads to faster rendering of views and decreased launch times for applications.

Additionally any template binding errors that may exist are reported during the build process allowing developers to resolve such issues BEFORE they ship their code.


**3. Minimise system intensive processes**

Handling asynchronous operations inside your applications?

Use callbacks or, given Ionic/Angular's built-in support, Promises and Observables wherever possible as these do not lock up your application or any underlying processes that are taking place.

Avoid the use of JavaScript timers such as SetInterval or setTimeout for asychronous operations and limit their presence in your application logic wherever possible as they are quite intensive on your device's system resources.

Implementing CSS animations?

Use CSS transitions and transforms together to take advantage of GPU hardware acceleration BUT do so sparingly as this can be very system intensive causing your device battery to drain while simultaneously raising thermal output.

Can service workers be used to handle background tasks?

What about using battery status to limit certain operations within your application? For example, you might want to prevent CSS/JS animations being triggered if the battery level falls below 60%.



**6. Data persistence**

Avoid local storage in favour of a database solution wherever possible.

Local storage has limitations in the quantity of data that can be stored, doesn't always behave consistently across different browsers and, bizarrely, sometimes "empties" itself without being prompted to do so.

Database solutions include the _Ionic Native SQLite plugin_( https://ionicframework.com/docs/native/sqlite/ ) or the incredibly powerful PouchDB ( https://pouchdb.com/ ) which can automatically synchronise application data with (if installed on your server) _CouchDB._ ( http://couchdb.apache.org/ )

I have written a number of articles *discussing building Ionic applications with PouchD*B. ( http://masteringionic.com/blog/archive/tag/pouchdb )


**8. Efficiently handle media content**

Can images be deployed as SVG's to cut down on file size (and aid with responsiveness over different screen sizes without requiring multiple different files to accomplish this)?

Have bitmap images been compressed to reduce file sizes - particularly if being loaded/requested remotely?

Could CSS sprites be used to optimise image sizes?

Would an application's images/video/audio assets be better handled through a Content Delivery Network?

When removing media from the component template view be sure to remove any and all references to that media element within the component logic (see point 5).

**9. Test, test and test some more**

Test non-cordova related application logic in your desktop browser with the developer tools of your choice (substitute the following examples using Safari with Google or Firefox if you use those browsers).

Make extensive use of console logging where relevant. Analyse network request/response times and test DOM rendering/browser repaint times with Safari's Timelines. Verify application logic flows with Safari's Debugger.

Run performance tests that measure timings for different operations (I.e. network requests, array iterations etc).

Use Xcode and Android simulators if you don't have a suite of testing devices (and how many developers can afford to continually add to and update the new devices being released every year?)

Alternatively investigate how your application performs on different devices using _opendevicelabs.com_. ( https://opendevicelab.com/ )

I would recommend these at a bare minimum but, as with all things development related, you can test and test to the point where it becomes an obsession.

Simply find what works for your project needs and run with that.



**How to optimize performance of Ionic 3.x PWA**

 - http://meumobi.github.io/ionic/2018/05/02/optimizing-performance-ionic-pwa.html
 