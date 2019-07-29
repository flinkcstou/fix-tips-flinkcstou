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
 
