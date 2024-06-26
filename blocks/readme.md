# Директория для фронт-енд компонентов проекта

Компоненты делятся на 2 основных вида: обычные компоненты и бандлы.

Бандлы регистрируются в entry.js. Чтобы удобнее их было отличать, называйте подобные компоненты начиная с "bundle-".
После запуска npm run build, бандлы превращаются в 2 файла - js и css и располагаются в директории local/assets/local.
Их можно уже подключать в нужные места на нужных страницах.

Компонент - директория с одноименными файлами, реализованные с помощью разных технологий: js, sass и mustache.

* mustache шаблон обязательно должен быть импортирован в js файле;  
* sass импортируется в js файл только в компоненте бандле. В остальных случаях sass нужно импортировать в другой sass;  
* js файл компонента может содержать просто js код, функцию или класс. Компоненты экспортируются в бандлы или другие компоненты.  

Служебные файлы:

* blocks/variables/_variables.sass - содержит основные переменные sass для проекта (шрифт, цвета, точки перегиба, etc);  
* blocks/mixins/_mixins.sass - содержит sass миксины проекта;  
* blocks/functions/functions.sass - содержит sass функции проекта;  
* blocks/helpers - содержит js функции-хелперы.  

## Технические нюансы:  

Для поддержки async, await используется idempotent-babel-polyfill. Подключите его в бандле, где необходим синтаксис
async, await.

```js
import 'idempotent-babel-polyfill'
```

Для аякс запросов можно использовать fetch. Но недавно выяснилось, что старые safari не полностью поддерживают fetch.
Поэтому используйте полифил:

```js
import { fetch as fetchPolyfill } from 'whatwg-fetch'
```