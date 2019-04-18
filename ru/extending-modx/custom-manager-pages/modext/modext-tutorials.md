---
title: 'Учебник по MODExt '
translation: developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials
---

## Введение

Поскольку MODExt расширяет существующий фреймворк (Ext JS), его документация пострадала, потому что авторы родительского фреймворка не имеют ничего общего с MODX, поэтому нет конкретных примеров того, как использовать этот фреймворк *внутри* MODX. Данные учебные пособия имеют целью представить MODExt (и, следовательно, Ext JS) и показать, как его можно использовать как в менеджере MODX, так и во внешнем интерфейсе ваших сайтов. Предполагается, что вы достаточно хорошо знакомы с JavaScript, чтобы следовать приведенным здесь примерам. Также можно надеяться, что дальнейшее продвижение повысит вашу уверенность в себе, и вы начнете выполнять серьезную работу с Ext JS в менеджере MODX или в ваших собственных пользовательских компонентах.

## Что такое Ext JS?

Большинство людей знакомы с  JavaScript, и jQuery стал королем библиотек. Но знайте: у jQuery уходит своими корнями в разработку эффектов и переходов для веб-страниц. Ext JS был основан для разработки *приложений*. Задумайтесь о менеджере MODX: это сложный набор поведений и взаимосвязанных окон, которые образуют единое целое. JQuery не был создан для таких вещей, но именно здесь Ext JS выглядит особенно ярко. Ext JS может сэкономить разработчикам *много* времени, когда дело доходит до создания таких приложений.

Чтобы помочь вам понять MODExt и Ext JS, я предлагаю вам по-другому взглянуть на веб-страницы. Когда вы создаете страницы с помощью Ext JS, вы как бы отказываетесь от традиционного подхода HTML. Это может сбить с толку, потому что вам больше не нужно создавать свои страницы с HTML - вы можете в конечном итоге создать целую страницу (или целое приложение), просто загрузив какой-то специальный JavaScript. Эта мысль может быть немного тревожной для любого из вас, кто привык к «старомодному» способу создания веб-страницы вручную. Подумайте об этом так: JavaScript позволяет вам манипулировать DOM, поэтому когда вы используете такой мощный инструмент как Ext JS, ваш браузер становится канвой, и несколько строк JavaScript могут рисовать его любым способом. HTML-код на вашей странице может стать полностью вторичным по отношению к тому, что происходит в JavaScript. Просто имейте это в виду, когда мы рассмотрим некоторые примеры здесь.

## Смотрите также

Фантастическая ссылка на Ext JS - [Ext JS в действии Иисуса Гарсии](http://www.amazon.com/Ext-JS-Action-Jesus-Garcia/dp/1935182110/ref=sr_1_1?ie=UTF8&qid=1370295075&sr=8-1&keywords=Ext+JS+in+Action).

![](/download/attachments/46137364/ext_js_cover.jpg?version=1&modificationDate=1370295179000)

Не берите в голову странную обложку с Франкенштейном 19-го века, танцующим брейк-данс - это на самом деле хорошая ссылка. Это полезно для MODX, в частности, потому что он охватывает Ext JS версии 3. Он был обновлен в 2011 году.

1. [Ext JS - Окна сообщений](extending-modx/custom-manager-pages/modext/modext-tutorials/1.-ext-js-tutorial-message-boxes)
2. [Ext JS - Ajax](extending-modx/custom-manager-pages/modext/modext-tutorials/2.-ext-js-tutorial-ajax-include)
3. [Ext JS - Анимация](extending-modx/custom-manager-pages/modext/modext-tutorials/3.-ext-js-tutorial-animation)
4. [Ext JS - Управление узлами](extending-modx/custom-manager-pages/modext/modext-tutorials/4.-ext-js-tutorial-manipulating-nodes)
5. [Ext JS - Панели](extending-modx/custom-manager-pages/modext/modext-tutorials/5.-ext-js-tutorial-panels)
6. [Ext JS - Расширенная сетка](extending-modx/custom-manager-pages/modext/modext-tutorials/7.-ext-js-tutoral-advanced-grid)
7. [Ext JS - Внутри CMP](extending-modx/custom-manager-pages/modext/modext-tutorials/8.-ext-js-tutorial-inside-a-cmp)