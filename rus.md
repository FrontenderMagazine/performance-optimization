![][1]

Задержки в производительности могут влиять на [вовлечённость][2] пользователей,
на их ощущения от [взаимодействия][3] с сайтом и [доходность][4] от него.
К счастью, команда проекта «Make The Web Faster» от Google
предложила набор наилучших практических [рекомендаций][5] для поддержания 
ваших страниц лёгкими, быстрыми и привлекательными. 
Они включают минификацию ресурсов вроде CSS и JavaScript, 
оптимизацию изображений, встраивание и удаление неиспользуемых стилей и т.д.

Если вы имеете полный доступ к вашему серверу, отличным вариантом для вас 
будет использование [модуля][7] [PageSpeed][6] для [Apache][8] и [Nginx][9] 
с фильтрами для многих из этих задач. Тем не менее, если не имеете, или вы 
понимаете, что модуля будет не достаточно, существует достаточно плагинов для 
систем сборок, использование которых, пожалуй, позволит восполнить пробелы с 
более точным управлением.

Ниже представлены [Grunt]-[10] и [Gulp][11]-плагины, которые команда проекта 
Yeoman регулярно использует в своих проектах. Мы постарались сохранить список 
целенаправленным и исключить прежние рекомендации, которые не представляют 
такой большой ценности, а того, что представлено здесь достаточно, чтобы 
помочь вам поддерживать ваши страницы и их ресуры настолько маленькими, на 
сколько это возможно.

**Примечание:** Генератор webapp для [Grunt][12] and [Gulp][13] от команды 
Yeoman включает плагины для оптимизации изображений, конкатенации и 
минификации HTML/CSS/JS. Мы считаем, это обеспечивает хорошую стартовую 
позицию, а эта статья охватывает плагины, которые выходят дальше за эту границу.

## Сжатие и оптимизация изображений

Среднестатистическая веб-страница сейчас занимает более [1.5 Мб][14], включая 
изображения, составляющие большую часть этого размера. Мы стремимся, чтобы 
размеры наших изображений были настолько малы, насколько это возможно, чтобы 
сократить время ожидания пользователя на их загрузку.

Правильный баланс сжатия и кадрирования позволяет по прежнему загружать 
изображения, словно это часть вашей страницы, за счёт сведения к минимуму 
времени загрузки на столько, на сколько это возможно. Это очень важно для 
пользователей мобильных устройств с ограниченными тарифными планами или 
медленным подключением.

#### Grunt

*   [grunt-contrib-imagemin][15]
*   [grunt-imageoptim][16] (только для OSX)

Почему два плагина? Ок, вот вам отличный [анализ][17] различий между ними. 
Можете выберать один, наиболее подходящий для вас.

#### Gulp

*   [gulp-imagemin][gulp-imagemin]

На момент написания статьи ещё не существовало плагина для Gulp, использующего 
ImageOptim.

**Примечание:** Ребята из Etsy выяснили, что добавление [всего лишь][18] 
160 Kб изображений на их страницы увеличивает отказ пользователей мобильных 
устройств на 12%. Если вы не можете сократить количество изображений на 
страницах, как минимум сделайте их оптимизацию.

## Генерация отзывчивых изображений для элемента `<picture>`

Если у вас отзывчивый сайт, адаптирующийся под различные устройства, вы также 
можете делать отзывчивыми и изображения.

Отдача излишне больших изображений браузеру может [влиять][19] на 
производительность загрузки и отображения, и это не единственные 
характеристики, которые могут пострадать от отдачи браузеру больших изображений.

Это одна из причин по которой нам нужно использовать отзывчивые изображения, и 
здесь мы рады наблюдать [srcset][20] — то, что, как мы надеемся, приведёт к 
полному внедрению элемента `<picture>`.

Существует несколько Grunt-плагинов, помогающих в рамках вашего процесса 
сборки проекта генерировать несколько изображений с различными разрешениями.

#### Grunt

*   [grunt-responsive-images][grunt-responsive-images] - используйте вместе с 
[Imager.js][Imager.js], элементом `<picture>` или полифил 
[picturefill][picturefill].
*   [grunt-clowncar][grunt-clowncar]

Кроме того, если вам нужно изменить размер больших изображений, для этого 
можете использовать [grunt-image-resize][21].

**Примечание:** Исследование Тима Кадлека в области отзывчивых изображений 
[привело к выводу][22], что использование отзывчивых изображений может 
привести к экономии до 72% на размере изображений.
Не смотря на то, что пока ещё рано делать выбор в пользу отзывчивости, BBC и 
Guardian используют Imager.js в качестве кросс-браузерного решения.

## Минификация SVG изображений

SVG файлы, созданные в редакторах обычно содержат большое количество 
избыточной информации (мета-данные, коментарии, скрытые элементы и т.д.).
Всё это может быть совершенно безвредно удалено или сконвертировано в более 
минималистичное представление, не влияя на отрисовку самого вектора.

#### Grunt

*   [grunt-svgmin][grunt-svgmin]

#### Gulp

*   [gulp-svgmin][gulp-svgmin]

## Генерация спрайтов

#### Grunt

*   [grunt-spritesmith][grunt-spritesmith]

#### Gulp

*   [gulp-sprite][gulp-sprite]

## Конвертация изображений в WebP

WebP это современный формат изображений, который предлагает сжатие изображений 
для веба с потерями и без. Изображения WebP со сжатием без потерь на 26% 
меньше по размеру, чем PNG и со сжатием с потерями на 25-34% меньше, чем JPEG. 
Это достаточно экономно и, к счастью, существуют Grunt- и Gulp-плагины 
кодирования WebP.

#### Grunt

*   [grunt-webp][grunt-webp]

#### Gulp

*   [gulp-webp][gulp-webp]

**Примечание:** Этот [тест][23], проведённый WebPageTest, говорит, что в 
сравнении с JPEG загрузка изображений WebP гораздо быстрее благодаря их 
маленькому размеру. 
В Chrome Web Store [выяснили][24], что использование WebP дало в среднем 30% 
экономии байтов, тем самым экономя им несколько терабайт трафика в день.

## Сборка SVG спрайтов с поддержкой для различных браузеров

### Grunt

*   [grunticon][grunticon]

### Gulp

*   [gulp-svgmin][gulp-svgmin]

Мы считаем, что встраивание изображений используя Data URI сейчас стало 
анти-паттерном, влекущим за собой [низкую][25] производительность на мобильных 
устройствах.

## Минификация CSS

Минификация устраняет лишние пробелы, переносы строк, отступы и символы, 
которые обычно не нужны в релизной версии файлов вашего продукта.
Сжатие ваших HTML-, CSS- и JS-файлов может улучшить парсинг, выполнение и время
загрузки. Касательно CSS мы рекомендуем:

#### Grunt

*    [grunt-contrib-cssmin][grunt-contrib-cssmin]

#### Gulp

*    [gulp-cssmin][gulp-cssmin]

## Удаление неиспользуемого CSS

В проектах, использующих CSS фреймворки вроде Bootstrap, Foundation и т.д. вы 
обычно не используете всё разнообразие доступных стилей.
Вместо того, чтобы пускать весь фреймворк в релиз, используйте UnCSS для 
удаления неиспользуемых вашими страницами стилей. Таким образом, некоторые 
разработчики облегчают свои таблицы стилей до 85%.

#### Grunt

*   [grunt-uncss][grunt-uncss]

#### Gulp

*   [gulp-uncss][gulp-uncss]

**Примечание:** Наиболее часто задаваемый разработчиками вопрос по поводу 
UnCSS или процесса удаления неиспользуемого CSS это может ли он также работать 
со стилями, внедряемыми в страницу динамически. Наш ответ — «да». UnCSS 
работает в паре с PhantomJS так, это стало возможным. Разработчики получают от 
[10][26] до [120 Кб][27] экономии на типичной Bootstrap-странице, и также 
хорошо UnCSS работает и с другими фреймворками.

## Встроенный CSS

Если внешние CSS-ресурсы для конкретной страницы достаточно малы, вы можете 
встроить их в вашу разметку, экономя при этом на дополнительных запросах к 
серверу. Встраивание небольшого количества CSS позволяет браузеру мгновенно 
приступить к отрисовке страницы.

#### Grunt

*   [grunt-inline-css][grunt-inline-css]

#### Gulp

*   [gulp-inline-css][gulp-inline-css]

## Комбинирование медиа-выражений

Хоть это и не является рекомендацией команды PageSpeed, но вы имеете 
возможность комбинировать медиа-выражения в единые определения. Мы сочли эти 
плагины полезными для обработки CSS, генерируемого препроцессорами, которые 
могут использовать вложенные определения медиа-запросов.

#### Grunt

*   [grunt-combine-media-queries][28]

#### Gulp

*   [gulp-combine-media-queries][29]

## JavaScript

### Минификация, сжатие JS

#### Grunt

*   [grunt-contrib-uglify][30]
*   [grunt-closure-compiler][31]

#### Gulp

*   [gulp-uglify][32]
*   [gulp-closure-compiler][33]

## RequireJS (оптимизация с r.js)

#### Grunt

*   [grunt-requirejs][grunt-requirejs]

#### Gulp

*   [RequireJS][RequireJS]

## Минификация HTML

#### Grunt

*   [grunt-contrib-htmlmin][grunt-contrib-htmlmin]

#### Gulp

*   [gulp-htmlmin][gulp-htmlmin]

## Простая конкатенация

#### Grunt

*   [grunt-contrib-concat][grunt-contrib-concat]

#### Gulp

*   [gulp-concat][gulp-concat]

## Общее сжатие для файлов/папок

#### Grunt

*   [grunt-contrib-compress][grunt-contrib-compress]

#### Gulp

*   [gulp-zip][gulp-zip]

## Сжатие Zopfli

Алгорим сжатия Zopfli — это библиотека сжатия с открытым исходным кодом, 
которая генерирует выходные данные на 3-8% меньше в сравнении с zlib при 
максимальном уровне сжатия.
Он лучше всего подходит для приложений, в которых данные сжимаются только один 
раз, а затем передаются по сети большое количество раз.

#### Grunt

*   [grunt-zopfli][grunt-zopfli]

#### Gulp

*   [gulp-zopfli][gulp-zopfli]

**Примечание:** Когда в Google Fonts начали использовать Zopfli, шрифты стали 
легче в среднем на 6%, а в некоторых случаях на 15%. По словам 
[Ильи Григорик][34], для Open Sans уменьшение размера было более чем на 10%, 
что сказалось на уменьшении времени на отрисовку и загрузку. 
Однако, изображения сжатые с Zofli декодируются дольше, чем обычные JPG. Эти 
показатели можно использовать для принятия решения о целесообразности 
использования WebP. 

## Встраивание CSS критического пути

Критический путь представляет собой код и ресурсы, необходимые для отрисовки 
контента, расположенного в верхней части страницы (*прим. пер.: дословно 
«above-the-fold» — до сгиба, т.е. первый экран страницы*) — то есть то, что 
ваши пользователи увидят в первую очередь, когда они станут загружать вашу 
страницу.
PageSpeed рекомендует встраивать ваши необходимые стили для улучшения 
производительности. 
В то время, как инструменты вроде [mod_pagespeed][35] достаточно высоко 
эффективны для достижения этого, оптимизировать необходимые стили другими 
инструментами гораздо сложнее.

Вы можете использовать PhantomJS со скриптами [speedreport][36], чтобы 
получить представление о том, какие стили отвечают за верхушку страницы и 
затем вручную оптимизировать их.

**Примечание:** Пол Кинлэн написал [букмарклет][37] для оценки стилей верхушки 
страницы, который тоже стоит посмотреть.

## Asset pipeline (авто-обработка всех оптимизаций)

Одним из инструментов, за которым нужно следить является [AssetGraph][38].

AssetGraph смотрит на проекты как на набор задач на графах, где узлами 
считаются наборы ресурсов (HTML, CSS, изображения, JS) и рёбрами — отношения 
между ними (теги img, a, script и т.д.).

Когда AssetGraph может определить, как проектные наборы ресурсов связаны друг 
с другом, он может выполнить автоматически большинство обычных оптимизаций 
производительности, которые разработчики могут хотеть достичь сами. Это 
работает, в частности, на маленьких проектах и над поддержкой для больших 
проектов в данный момент идёт работа.

#### Grunt

*   [grunt-reduce][grunt-reduce]

#### Gulp

Пользователи Gulp должны использовать непосредственно AssetGraph.

## Сравнительный анализ

Приведённые ниже бенчмарк-плагины полезны для использования в качестве части 
реализации подхода непрерывной интеграции (Continuous Integration). Не смотря 
на то, что они в настоящее время доступны только для Grunt, вы можете 
использовать [gulp-grunt][39] для запуска Grunt-тасков через Gulp. Мы 
рекомендуем:

*   [grunt-pagespeed][40] - превосходен для автоматического определения ваших 
количества очков PageSpeed как часть непрерывной интеграции.
   
*   [grunt-topcoat-telemetry][41] - получение гладкости, времени загрузки и 
другой статистики из Telemetry, как часть процесса непрерывной интеграции. 
Это может помочь вам настроить панель сравнительного анализа 
производительности, похожую на ту, что используют в [TopCoat][42].

*   [grunt-wpt][43] - непрерывная интеграция с очками WebPageTest.
*   [grunt-phantomas][44] - время ответа на запросы, на ответы, время загрузки 
первого изображения/CSS/JS, время события готовности DOM и другое.

## Framework Optimization

#### Grunt

*   [grunt-ngmin][grunt-ngmin]
*   [grunt-react][grunt-react]
*   [grunt-vulcanize][grunt-vulcanize] — хорош для конкатенации веб-компонентов


#### Gulp

*   [gulp-ngmin][45]
*   [gulp-react][46]
*   [gulp-vulcanize][47]

#### Misch

*   [gulp-google-cdn][gulp-google-cdn]
*   [gulp-size][gulp-size]

## Заключение

Задержки в производительности могут влиять на вовлечение пользователя и его 
впечатления от взаимодействия с ресурсом. Уделите время на эксперименты с плагинами 
для оптимизации производительности, узнайте, какие практические выгоды они 
могут дать вашим проектам. 

Посетители ваших сайтов будут счастливее в результате мгновенного отклика, да 
и вообще, быстрый веб — лучше для всех.

~ Эдди Османи

*Выражает благодарности Sindre Sorhus, Pascal Hartig и Stephen Sawchuk за их отзывы*

 [1]: img/tasks.1c7b.jpg
 [2]: https://twitter.com/igrigorik/status/300226402496704512

 [3]: http://www.smashingmagazine.com/2013/06/10/pinterest-paint-performance-case-study/
 [4]: https://speakerdeck.com/lara/design-for-performance
 [5]: https://developers.google.com/speed/docs/insights/rules
 [6]: https://developers.google.com/speed/pagespeed
 [7]: https://developers.google.com/speed/pagespeed/module
 [8]: https://developers.google.com/speed/pagespeed/module/download

 [9]: https://developers.google.com/speed/pagespeed/module/build_ngx_pagespeed_from_source
 [10]: http://gruntjs.com
 [11]: http://gulpjs.com
 [12]: http://github.com/yeoman/generator-webapp
 [13]: http://github.com/yeoman/generator-gulp-webapp

 [14]: http://httparchive.org/interesting.php?a=All&l=Aug%2015%202013#bytesperpage
 [15]: https://github.com/gruntjs/grunt-contrib-imagemin
 [16]: https://github.com/JamieMason/grunt-imageoptim
 [17]: http://jamiemason.github.io/ImageOptim-CLI

 [18]: http://programming.oreilly.com/2014/01/web-performance-is-user-experience.html
 [19]: http://timkadlec.com/2013/11/why-we-need-responsive-images-part-deux/

 [20]: http://blog.chromium.org/2014/02/chrome-34-responsive-images-and_9316.html?m=1
 [21]: https://www.npmjs.org/package/grunt-image-resize
 [22]: http://timkadlec.com/2013/06/why-we-need-responsive-images/

 [23]: http://www.webpagetest.org/video/compare.php?tests=130125_6N_KZA%2C130125_NH_KZ8&thumbSize=200&ival=100&end=full

 [24]: http://www.igvita.com/2013/03/07/faster-smaller-and-more-beautiful-web-with-webp/
 [25]: http://www.mobify.com/blog/data-uris-are-slow-on-mobile/
 [26]: https://twitter.com/efexen/status/438672726996574209
 [27]: https://twitter.com/thisbetom/status/432575411138998273
 [28]: https://npmjs.org/package/grunt-combine-media-queries
 [29]: https://www.npmjs.org/package/gulp-combine-media-queries
 [30]: https://github.com/gruntjs/grunt-contrib-uglify
 [31]: https://github.com/gmarty/grunt-closure-compiler
 [32]: https://github.com/terinjokes/gulp-uglify
 [33]: https://github.com/sindresorhus/gulp-closure-compiler
 [34]: https://plus.google.com/+IlyaGrigorik/posts/1sxencNkbNS
 [35]: https://code.google.com/p/modpagespeed/
 [36]: https://github.com/r3b/speedreport/

 [37]: http://addyosmani.com/blog/detecting-critical-above-the-fold-css-with-paul-kinlan-video/
 [38]: https://github.com/assetgraph/assetgraph
 [39]: https://npmjs.org/package/gulp-grunt
 [40]: https://npmjs.org/package/grunt-pagespeed
 [41]: https://github.com/topcoat/topcoat-grunt-telemetry
 [42]: http://bench.topcoat.io/
 [43]: https://npmjs.org/package/grunt-wpt
 [44]: https://www.npmjs.org/package/grunt-phantomas
 [45]: https://github.com/sindresorhus/gulp-ngmin
 [46]: https://github.com/sindresorhus/gulp-react
 [47]: https://github.com/sindresorhus/gulp-vulcanize
[grunt-contrib-cssmin]: https://github.com/gruntjs/grunt-contrib-cssmin
[gulp-cssmin]: https://www.npmjs.org/package/gulp-cssmin
[grunt-uncss]: https://github.com/addyosmani/grunt-uncss
[gulp-uncss]: https://github.com/ben-eb/gulp-uncss
[grunt-inline-css]: https://github.com/jgallen23/grunt-inline-css
[gulp-inline-css]: https://www.npmjs.org/package/gulp-inline-css/
[grunt-requirejs]: https://github.com/asciidisco/grunt-requirejs
[RequireJS]: http://requirejs.org/
[grunt-contrib-htmlmin]: https://github.com/gruntjs/grunt-contrib-htmlmin
[gulp-htmlmin]: https://github.com/jonschlinkert/gulp-htmlmin
[grunt-contrib-concat]: https://github.com/gruntjs/grunt-contrib-concat
[gulp-concat]: https://www.npmjs.org/package/gulp-concat
[grunt-contrib-compress]: https://www.npmjs.org/package/grunt-contrib-compress
[gulp-zip]: https://github.com/sindresorhus/gulp-zip
[grunt-zopfli]: https://github.com/mathiasbynens/grunt-zopfli
[grunt-reduce]: https://github.com/Munter/grunt-reduce
[grunt-ngmin]: https://npmjs.org/package/grunt-ngmin
[grunt-react]: https://npmjs.org/package/grunt-react
[grunt-vulcanize]: https://npmjs.org/package/grunt-vulcanize
[gulp-google-cdn]: https://github.com/sindresorhus/gulp-google-cdn
[gulp-size]: https://github.com/sindresorhus/gulp-size
[gulp-imagemin]: https://github.com/sindresorhus/gulp-imagemin
[grunt-responsive-images]: https://github.com/andismith/grunt-responsive-images
[Imager.js]: https://github.com/BBC-News/Imager.js/
[picturefill]: https://github.com/jansepar/picturefill
[grunt-clowncar]: https://npmjs.org/package/grunt-clowncar
[grunt-svgmin]: https://github.com/sindresorhus/grunt-svgmin
[gulp-svgmin]: https://www.npmjs.org/package/gulp-svgmin
[grunt-spritesmith]: https://www.npmjs.org/package/grunt-spritesmith
[gulp-sprite]: https://www.npmjs.org/package/gulp-sprite
[grunt-webp]: https://github.com/somerandomdude/grunt-webp
[gulp-webp]: https://github.com/sindresorhus/gulp-webp
[grunticon]: https://github.com/filamentgroup/grunticon
