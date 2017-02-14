---
layout: post
title: CSS табуляция без фонового изображения
category: CSS
tags: css, tabulation
authors: fdkitamory
slug: css-tabulation
---

Несколько раз встречался с необходимостью делать табуляцию, google показал в качестве популярного варианта использование фонового изображения,  им  и воспользовался. Но у такого варианта один недостаток - при изменении шрифта требуется изменить фоновое изображение, да и с появлением дисплеев высокой чёткости катинка становится размытой. Сделал без картинок.
<!-- PELICAN_END_SUMMARY -->

Заменой фону с картинкой стал псевдо элемент **[::after](http://htmlbook.ru/css/after)** для контейнера строки. В него упаковываем много точек и позиционируем через position: absolute.
Вариант тоже не надёжный, но внешний вид точек изменяется указанием стилей для шрифта. Пример кода ниже, подробно [тут](http://fdkitamory.com/examples/css-tabulation/) или на [гитхабе](https://github.com/fdkitamory/css-tabulation).

В перспективе дописать до многострочной реализации. Но чуть позже.

**HTML:**

	:::html
		<ul class="tab">
            <li class="tab__row">
                <div class="tab__col">Текст заголовка</div>
                <div class="tab__col tab__page">с. 53</div>
            </li>
            <li class="tab__row">
                <div class="tab__col">Текст заголовка</div>
                <div class="tab__col tab__page">с. 53</div>
            </li>
            <li class="tab__row">
                <div class="tab__col">Текст заголовка</div>
                <div class="tab__col tab__page">с. 53</div>
            </li>
            <li class="tab__row">
                <div class="tab__col">Текст заголовка</div>
                <div class="tab__col tab__page">с. 53</div>
            </li>
        </ul>


**CSS:**

	:::css
		.tab{
            width: 400px;
            padding: 0; margin: 0;
        }
            .tab__row{
                position: relative;
                height: 40px;
                background: #d0d0d0;
                line-height: 40px;
                list-style: none;
                z-index: 0;
            }
                .tab__row:after{
                    content: "..............................................................................................";
                    position: absolute;
                    top: 0;left: 0;
                    height: 40px;
                    z-index: -1;
                }
                .tab__row:nth-child(2n),
                .tab__row:nth-child(2n) .tab__col{
                    background: #fff;
                }
                    .tab__col{
                        float: left;
                        height: 40px;
                        background: #d0d0d0;
                    }
                        .tab__page{
                            float: right;
                            text-align: right;
                        }
