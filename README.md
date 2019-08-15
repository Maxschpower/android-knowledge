# Android Projects Style Guide

# 0. Используемые библиотеки
 * [RxJava2](https://github.com/ReactiveX/RxJava/tree/2.x) - библиотека с реактивными расширениями для JVM. __Обязательно__ используется в каждом проекте использующем сетевые запросы
 * [AdapterDelegates](https://github.com/sockeqwe/AdapterDelegates) - сильно упрощает множеством различных видов ViewType в одном RecyclerView
 * [Cicerone](https://github.com/terrakok/Cicerone) - упрощает работу с навигацией в приложении

Архитектурные библиотеки -
 * MVP - [Moxy](https://github.com/Arello-Mobile/Moxy)
 * MVVM - [Lifecycle компоненты](https://developer.android.com/jetpack/androidx/releases/lifecycle)

# 1. Проектные рекомендации

## 1.1 Структура проекта

Новые проекты должны следовать структуре Android Gradle описанной в [Android Gradle plugin user guide](http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Project-Structure). [GitFox ](https://gitlab.com/terrakok/gitlab-client) является отличным примером архитектуры.

## 1.2 Именование файлов

### 1.2.1 Файлы классов

Названия классов пишутся в [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

Классы наследуемые от Android компонента должны оканчиваться названием наследуемого компонента:  `SignInActivity`,  `SignInFragment`,  `ImageUploaderService`,  `ChangePasswordDialog`.

### 1.2.2 Файлы ресурсов

Названия ресурсов пишутся в **lowercase_underscore**.

#### 1.2.2.1 Drawable файлы

Конвенция именования для графических ресурсов:


| Тип          | Префикс           |		Пример           |
|--------------| ------------------|-----------------------------|
| Action bar   | `ab_`             | `ab_stacked.9.png`          |
| Button       | `btn_`	           | `btn_send_pressed.9.png`    |
| Dialog       | `dialog_`         | `dialog_top.9.png`          |
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`	           | `ic_star.png`               |
| Menu         | `menu_	`          | `menu_submenu_bg.9.png`     |
| Notification | `notification_`   | `notification_bg.9.png`     |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |

Конвенция именования для иконок (взята с [Android iconography guidelines](http://developer.android.com/design/style/iconography.html)):

| Тип                      	  | Префикс            | Пример                       |
| --------------------------------| ----------------   | ---------------------------- |
| Icons                           | `ic_`              | `ic_star.png`                |
| Launcher icons                  | `ic_launcher`      | `ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Status bar icons                | `ic_stat_notify`   | `ic_stat_notify_msg.png`     |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |

Конвенция именования для селекторов:

| Состояние    | Суффикс         | Пример                      |
|--------------|-----------------|-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |


#### 1.2.2.2 Layout файлы

Файлы экранов должны начинаться с названия компонента, используемого для отображения этого экрана. Например, создавая верстку для `SignInActivity`, название файла должно быть `activity_sign_in.xml`.

| Компонент        | Имя класса             | Название файла                |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |

Немного отличается именование файлов используемых для использования в `Adapter`, например в  `RecyclerView`. В данном случае название должно начинаться с `item_`.

#### 1.2.2.3 Menu файлы

По аналогии с файлами экранов, файлы меню должны включать название Android компонента, в котором будут использоваться. Например, если меню создается для `UserActivity`, то название файла должно быть `activity_user.xml`

Файл не должен начинаться с `menu` так как он уже располагается в папке `menu`.

# 2. Code guidelines

## 2.1 Стиль написания Kotlin кода
Стиль написания Kotlin кода смотреть на [официальном сайте Kotlin](https://kotlinlang.org/docs/reference/coding-conventions.html)

## 2.2 Правила стиля XML

### 2.1.1 Использование ``/>``

Если XML элемент не имеет ничего внутри себя, __обязательно__ нужно использовать ``/>`` для закрытия тэга.

Это правильно:

```xml
<TextView
	android:id="@+id/text_view_profile"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content" />
```

Это __неправильно__ :

```xml
<!-- Don\'t do this! -->
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```


### 2.1.2 Именование ресурсов

Названия и id ресурсов пишутся в __camelCase__, так как благодаря kotlin extensions можно напрямую обращаться к view по ее ID, не вызывая findViewById().

#### 2.1.2.1 ID naming

ID должны начинаться с названия экрана, на котором они применяются. Например:


| Экран                 |Элемент       |ID                       |
|-----------------------|--------------|-------------------------|
| `ProfileActivity`     | `TextView`   |`profileName`            |
| `RegistrationFragment`| `Button`     |`registrationLoginButton`|
| `NewsDialog`          | `ImageView`  |`newsImage`              |
| `SettingsFragment`    | `ImageButton`|`settingsSaveButton`     |


#### 2.1.2.2 Строки

Названия строк должны начинаться с названия места их применения. Например `registration_email_hint` или `registration_name_hint`. Если строка __не относится__ к определенному экрану, тогда нужно использовать следующие правила:


| Префикс              | Описание                           |
| ---------------------| -----------------------------------|
| `error_`             | Сообщение об ошибке                |
| `msg_`               | Обычное информационное сообщение   |
| `title_`             | Название чего-либо                 |
| `action_`            | Действия по типу "Сохранить" и т.д.|



#### 2.1.2.3 Стили и темы

Названия пишутся в __UpperCamelCase__.

### 2.1.3 Attributes ordering

Старайтесь группировать похожие атрибуты. Хороший порядок атрибутов :

1. ID
2. Стиль
3. Ширина и высота элемента 
4. Остальные атрибуты в алфавитном порядке

## 2.2 Правила написания тестов

### 2.2.1 Юнит тесты

Классы тестов должны начинаться с названия тестируемого функционала и оканчиваться словом `Test`. Например класс для тестирования `DatabaseHelper` должен называться `DatabaseHelperTest`.

Тестовые методы с аннотацией `@Test` должны начинаться с названия тестируемой функции, заканчивая ожидаемым результатом.

* Шаблон: `@Test void methodNamePreconditionExpectedBehaviour()`
* Пример: `@Test void signInWithEmptyEmailFails()`

Иногда класс может содержать большое количество тестируемых методов. В данном случае следует разбить тестовый класс на несколько. Например, если `DataManager` содержит много тестируемых методов, то нам следует разбить класс теста на `DataManagerSignInTest`, `DataManagerLoadUsersTest`, и т.д.

# 3. Работа в git системе
## 3.1 Ветки
### 3.1.1 Виды веток
Для работы в git системе в компании используются следующие ветки:
* Master - корневая ветка проекта. В ней содержатся __исключительно__ релизные версии. Может быть только одна ветка Master.
* Develop - ветка для разработки. В ней должны находится только __законченные__ фичи. Может быть только одна ветка Develop. Идет от __master__ ветки.
* Feature - ветки для разработки фич. В них происходит разработка отдельных фич. Может быть большое количество. Обязательно должна идти от ветки __develop__.
* Fix - ветки для внесения исправлений. Должна ответвляться либо от __develop__, либо от __master__.

### 3.1.2 Правила ведения веток

#### 3.1.2.1 Master
В ``master`` ветку имеет право заливать изменения __ТОЛЬКО__ тимлид. В этой ветке находятся релизные версии проекта из ветки ``develop``.

#### 3.1.2.2 Develop
В ветку ``develop`` входят фичи из ``feature`` веток. 

#### 3.1.2.3 Feature
В этой ветке происходит вся работа. Обычно, ``feature`` начинают с последнего коммита в ветке ``develop``, но если для работы новой ветки необходимы изменения из еще не влитой в ``develop`` фичи, можно создать ``feature`` от нее. Название ветки обязательно должно начинаться с ``feature/`` и быть осознанным, чтобы любой другой разработчик мог по названию понять цель создания ветки. Например:


| Цель                          | название ветки |
|-------------------------------|----------------|
| Разработка модуля авторизации | feature/auth   |
| Разработка экрана новостей    | feature/news   |


 Законченные фичи вливаются в ``develop`` и закрываются только с помощью **pull request**, в ходе которого тимлид проведет ревью кода и скажет, если нужно исправить какие-либо моменты в коде.
 
N. B.
Pull request'ы принимаются тимлидами __только по вторникам и четвергам__.

#### 3.1.2.4 Fix
Эта ветка используется для внесения исправлений в ``develop`` и ``master``. Так же как и ``feature``, ветка ``fix`` должна начинаться с ``fix/`` и названием объяснять вносимые исправления.
