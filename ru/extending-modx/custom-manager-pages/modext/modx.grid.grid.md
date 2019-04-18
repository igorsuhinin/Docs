---
title: MODx.grid.Grid
translation: extending-modx/custom-manager-pages/modext/modx.grid.grid
---

## MODx.grid.Grid

**Расширяет:** Ext.grid.EditorGridPanel

**Основные характеристики:** функциональность коннектора; позволяет легко интегрировать элементы панели инструментов и MODx.Window; встроенная функциональность контекстного меню.

При создании этого экземпляра в интерфейсе с вкладками рекомендуется установить в своей конфигурации protectRender: true, чтобы предотвратить проблемы с отображением JS.

![](/download/attachments/18678079/grid.png?version=1&modificationDate=1302187849000)

Сетки MODExt используются для отображения табличных данных в комплекте с ColumnModel, верхней панелью инструментов (tbar) и нижней панелью инструментов (bbar). Они также имеют встроенную поддержку постраничного разбиения. Сетки заполняются удаленно по запросу в коннектор, возвращающего объект JSON. Отображение контекстного меню правой кнопкой мыши для каждой строки может быть легко достигнуто включением ключа «menu» для каждой строки данных в вашем процессоре:

```php
foreach( $items as $item ) {
    $data[] = array(
        'id'    => $obj->get( 'id' ),
        'name'  => $obj->get( 'name' ),
        'menu'  => array(
            array(
                'text'      => $modx->lexicon( 'my_lexicon' ),
                'handler'   => 'this.myHandler'
            )
        )
    );
}
```

Приведенный выше код создает контекстное меню для каждого элемента, текст которого является ключом лексикона, соответствующим «my_lexicon», а обработчик - функцией myHandler, зарегистрированной в вашем объекте Grid.

Альтернативно (и предпочтительно) меню могут быть созданы путем расширения вашей сетки JS и добавления метода «getMenu»:

```javascript
getMenu: function() {
    var m = [];
    m.push({
        text: _('my_lexicon_key')
        ,handler: this.myHandler
    });
    return m;
}
```

Возвращение массива элементов в методе getMenu автоматически добавит элементы в контекстное меню.

Сетки Revolution 2.0.x не могут просто вернуть массив - им нужно будет вызвать «this.addContextMenuItem(m);» перед концом функции. Возвращающий массив был добавлен в версии 2.1.

## Специфичные для MODExt параметры

Прежде всего, MODx.grid.Grid извлекает свои данные удаленно через параметр конфигурации "url". Он также загружает baseParams в вызов, который по умолчанию выглядит как:

```javascript
baseParams: { action: 'getList' }
```

Вы можете переопределить baseParams в параметре конфигурации.

MODx.grid.Grid добавляет несколько уникальных параметров, которых нет в типичных объектах Ext.grid.Grid:

Название | Описание | Значение по умолчанию
--- | --- | ---
URL | URL-адрес коннектора для загрузки этой сетки. | 
paging | Если true, включит постраничное разделение и автоматически добавит PagingToolbar внизу сетки. | true
pageSize | Количество элементов на странице, если paging == true. По умолчанию используется системная настройка default_per_page, которая равна 20. | 20
pageStart | Начальный индекс постраничного разбиения. | 0
showPerPage | Показывать или нет текстовое поле «На страницу». По умолчанию true. | true
pagingItems | Любые элементы, добавляемые справа от текстового поля «На страницу» на панели инструментов подкачки. Полезно для добавления дополнительных кнопок. | []
grouping | Если true, автоматически включит группировку по этой сетке. | false
groupBy | Столбец для группировки. Обратите внимание, что столбец должен быть в модели столбца. | name
pluralText | Текст для множества элементов в сгруппированном столбце, например: «Строки» | Records
singleText | Текст для одного количества элементов в сгруппированном столбце, а именно: «Строка» | Record
sortBy | Столбец по умолчанию для сортировки при группировке и remoteSort установленном в true. | id
sortDir | Направление сортировки по умолчанию при группировке и remoteSort установленном в true | ASC
preventRender | Предотвратить рендеринг сетки. Полезно при размещении сетки на панелях или вкладках. | 1
autosave | Если установлено значение true, будет автоматически запускаться процессор 'updateFromGrid' (или процессор в параметре конфигурации saveUrl) для этого коннектора при выполнении встроенного редактирования в сетке. | false
saveUrl | URL-адрес коннектора для вызова при встроенном редактировании с включенным автосохранением. | Значение config.url
save_action | Действие процессора для вызова при inline-редактировании с включенным автосохранением | updateFromGrid
saveParams | JS-объект параметров, который также отправляется в saveUrl при автосохранении или при использовании метода удаления MODx.grid.Grid. | {}
save_callback | После автосохранения запустите этот метод. | null
preventSaveRefresh | Если автосохранение имеет значение true, после сохранения будет препятствовать обновлению сетки. Используется для более плавного редактирования. | 1
primaryKey | Если у ваших элементов сетки есть первичный ключ, который не является идентификатором, установите его здесь. | id
storeId | Пользовательский идентификатор для предоставления хранилища в данной сетке. По умолчанию будет использоваться уникальный Ext ID. | Ext.id()

Полный список всех параметров, не перечисленных здесь, см. в документации [ExtJS](http://sencha.com).

## Пользовательские события

MODx.grid.Grid добавляет несколько дополнительных событий, не найденных в объектах Ext.grid.Grid:

Название | Описание
--- | ---
beforeRemoveRow | Запускается перед удалением строки при вызове метода remove() в сетке (обычно это делается в контекстном меню)
afterRemoveRow | Запускается после удаления строки при вызове метода remove() в сетке (обычно это делается в контекстном меню)
afterAutoSave | Запускается после сохранения с помощью встроенного редактирования, если для автосохранения установлено значение true.

## Другие уникальные функции

Сетки MODExt имеют довольно много других функций.

### Пользовательские сообщения об исключениях

Если возвращаемый JSON не является допустимой коллекцией хранилища данных и содержит параметр «message», для него будет задано значение emptyText для сетки и будет отображаться в качестве первой строки сетки. Обычно используется $modx->error->failure('Сообщение здесь') в ваших процессорах.

### loadWindow

Автоматически загружает и показывает окно любого данного xtype:

```javascript
grid.loadWindow({
  xtype: 'my-xtype-for-the-window'
  ,blankValues: true /* очищает значения окна, полезно для новых оконных объектов, установите в false для обновления окон */
});
```

Если blankValues не установлен в true, этот метод автоматически передаст данные текущей выбранной строки также в окно, установив его значения в форме (при условии, что ваше окно расширяет [MODx.Window](extending-modx/custom-manager-pages/modext/modx.window "MODx.Window").)

### remove

MODx.grid.Grid поставляется с пользовательским методом под названием «remove», который автоматически запускает AJAX-запрос к вашему коннектору, установленному в config.url с действием «remove», и ID (или primaryKey, установленный в конфигурации) выбранной строки. Это полезно для контекстных меню.

Метод принимает один параметр - текст - текст, отображаемый в диалоговом окне подтверждения, которое запрашивает пользователя, хотят ли они удалить строку перед тем, как это сделать. Событие beforeRemoveRow вызывается до загрузки диалогового окна подтверждения.

```javascript
grid.remove("Вы уверены, что хотите удалить этот объект?");
```

### config

Это пользовательский метод, который позволяет открыть диалоговое окно подтверждения перед выполнением действия:

```javascript
grid.confirm("approve","Вы уверены, что хотите принять эту статью?");
```

Как и при удалении, метод принимает идентификатор или primaryKey выбранной в данный момент строки и отправит его на процессорное действие, указанное в первом параметре метода подтверждения. Когда выполнится, метод обновит сетку.

### refresh

Пользовательский метод, который будет обновлять сетку при каждом запуске.

### encodeModified

Метод вернет объект JSON всех измененных (грязных) строк и полей. Полезно, если для автосохранения установлено значение false.

### encode

Метод вернет объект JSON для всех строк.

## Смотрите также

1. [Объект MODExt MODx](extending-modx/custom-manager-pages/modext/modext-modx-object)
2. [Учебник по MODExt ](extending-modx/custom-manager-pages/modext/modext-tutorials)
    1. [Ext JS - Окна сообщений](extending-modx/custom-manager-pages/modext/modext-tutorials/1.-ext-js-tutorial-message-boxes)
    2. [Ext JS - Ajax](extending-modx/custom-manager-pages/modext/modext-tutorials/2.-ext-js-tutorial-ajax-include)
    3. [Ext JS - Анимация](extending-modx/custom-manager-pages/modext/modext-tutorials/3.-ext-js-tutorial-animation)
    4. [Ext JS - Управление узлами](extending-modx/custom-manager-pages/modext/modext-tutorials/4.-ext-js-tutorial-manipulating-nodes)
    5. [Ext JS - Панели](extending-modx/custom-manager-pages/modext/modext-tutorials/5.-ext-js-tutorial-panels)
    6. [Ext JS - Расширенная сетка](extending-modx/custom-manager-pages/modext/modext-tutorials/7.-ext-js-tutoral-advanced-grid)
    7. [Ext JS - Внутри CMP](extending-modx/custom-manager-pages/modext/modext-tutorials/8.-ext-js-tutorial-inside-a-cmp)
3. [MODx.combo.ComboBox](extending-modx/custom-manager-pages/modext/modx.combo.combobox)
4. [MODx.Console](extending-modx/custom-manager-pages/modext/modx.console)
5. [MODx.FormPanel](extending-modx/custom-manager-pages/modext/modx.formpanel)
6. [MODx.grid.Grid](extending-modx/custom-manager-pages/modext/modx.grid.grid)
7. [MODx.grid.LocalGrid](extending-modx/custom-manager-pages/modext/modx.grid.localgrid)
8. [MODx.msg](extending-modx/custom-manager-pages/modext/modx.msg)
9. [MODx.tree.Tree](extending-modx/custom-manager-pages/modext/modx.tree.tree)
10. [MODx.Window](extending-modx/custom-manager-pages/modext/modx.window)
