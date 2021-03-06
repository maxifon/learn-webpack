# Добавить в проект Webpack: 
1. `npm init`
    > Отвечаем на вопросы в терминале. На основании ответов будет сгенерирован файл `package.json`
2. `npm install -D webpack webpack-cli`
    > Флаг `-D` означает, что зависимости сохраняются только для разработки. То есть мы устанавливаем 2 инструмента, которые не пойдут в финальное приложение, а нужны для упрощения разработки. И попадают они в раздел `devDependencies` файла `package.json`.
    
    > `webpack` - пакет с корневым функционалом
                                                                                                                                                                                                                                                                                                                 
    > `webpack-cli` - пакет, позволяющий через терминал управлять `webpack`'ом.

## Работа с `webpack`
С ним можно работать как через терминал, так и файл `webpack.config.js` ( файл с таким названием webpack ищет по умолчанию в корне приложения ). Второй способ работы с `webpack` удобнее.

`webpack.config.js` используется только для разработки, он не попадает в финальное приложение.

1. Настраиваем файл `webpack.config.js` : внутри `module.exports {...}` указываем `entry`, `output`.
2. Выполняем в терминале команду `webpack`.
    > Эта команда соберет приложение в указанную в `output` директорию (обычно `dist`).
    Если команда не работает, то в `webpack.config.js` внутрь секции `script` нужно добавить строчку `"run": "webpack"`, чтобы получилось следующее:
    
    ```
    "scripts": {
      ...
      "webpack": "webpack",
      ...
    }                                     
    ```  
   
   > И запустить команду `webpack` через idea, нажав на зеленый значок запуска, либо выполнив команду `npm run webpack`.
## Изменения в файлах при использовании webpack
`index.html` - в данном файле удаляем 
```
<script src="js/analytics.js"></script>
<script src="js/Post.js"></script>
```

И добавляем строку 
```
<script src="bundle.js"></script>
```

Копируем `index.html` в `dist`.

## Ошибки

В браузере не виден файл `analytics.js`.

*Причина*: файл `analytics.js` не попал в сборку `bundle.js`, с которым и работает `index.html`, так как `analytics.js` не импортируется в `index.js`, являющийся 'entry point' в `webpack.config.js`. Webpack `analytics.js` игнорирует.  
