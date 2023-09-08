### Android Netology 5
*****

#### Домашнее задание к занятию «1.2. Сетевые запросы: Main Thread & Background»

<details close><summary> Задача Likes </summary>
    <br>
    
Предоставлены описания API для реализации:

1. Добавление лайка:
    `POST /api/posts/{id}/likes`

2. Удаление лайка:
    `DELETE /api/posts/{id}/likes`

Где **{id}** - это идентификатор поста.

В ответ на оба запроса сервер присылает JSON обновленного поста, который можно использовать для отображения измененного поста в ленте.

В проекте реализвана функциональность простановки/снятия лайка. Для этого используется [код сервера с лекции](https://github.com/netology-code/andin-code/tree/master/02_threads/server).

> После выполнения запроса список постов обновляется, для отображения пользователю актуального количества лайков.

</details>
<details close><summary> Задача Swipe to Refresh* </summary>
    <br>
    
Реализована функциональность `Swipe To Refresh` в списках:

- Пользователь "тянет" сверху вниз список (или любое другое View)
- Появляется иконка обновления
- Список обновляется

>Для этого:
>
>1. Добавлена необходимая [зависимость в build.gradle](https://developer.android.com/jetpack/androidx/releases/swiperefreshlayout)
>2. ***RecyclerView*** завёрнут `в androidx.swiperefreshlayout.widget.SwipeRefreshLayout`
>3. `OnRefreshListener` заново запрашивает все посты с сервера
   
</details>

#### Домашнее задание к занятию «2.2 Современные подходы работы с многопоточностью»

<details close><summary> Задача OkHttp enqueue </summary>
    <br>
    
Перевод функциональности проекта с использования функции thread на enqueue из OkHttp. После выполнения запроса список постов обновляется, для отображения пользователю актуального количества лайков.

</details>

#### Домашнее задание к занятию «2.3 Многопоточность в Android»

<details close><summary> Задача Glide </summary>
    <br>
    
Реализовано отображение аватарок в приложении с использованием [проекта сервера](https://github.com/netology-code/andin-code/tree/master/06_android).

В качестве библиотеки для загрузки изображений использована библиотека ***Glide***.

</details>

<details close><summary> Задача Rounded </summary>
    <br>
    
Для реализации круглых аватарок, среди [методов трансформации](https://bumptech.github.io/glide/doc/transformations.html) был выбран наиболее подходящий класс *CircleCrop*.

</details>

<details close><summary> Задача Attachments* </summary>
    <br>
    
Для тех постов, у которых есть вложения (типа - *IMAGE*) ***attachment*** на сервере, реализовано отображение соответствующей картинки в посте :

![](https://github.com/netology-code/andin-homeworks/blob/master/06_android/pic/attachment.png?raw=true)

</details>

#### Домашнее задание к занятию «2.4 Retrofit (CRUD)»

<details close><summary> Задача Buggy Server </summary>
    <br>
    
Рассмотрен альтернативный (но очень частый) сценарий - [сервер](https://github.com/netology-code/andin-homeworks/blob/master/07_crud/server) периодически (а именно в 50% случаев) присылает не 2xx коды ответа. С его использованием реализована обработка подобного рода ошибок методом вывода на экран пользователя **Snackbar'а**

</details>

#### Домашнее задание к занятию «3.3 Coroutines в Android»

<details close><summary> Задача remove & likes </summary>
    <br>
    
Реализована функциональность удаления и проставления лайков.

Логика работы:
1. Сначала была модифицирована запись в локальной БД
2. Затем отправляется соответствующий запрос в API (HTTP)
Также произведена обработка ошибок и кнопка `Retry`, в случае, если запрос в API завершился с ошибкой (в том числе в случае отсутствия сетевого соединения*).

Примечание*: для этого не обязательно перезапускать сервер, достаточно отключить сеть в шторке телефона/эмулятора.

</details>

#### Домашнее задание к занятию «3.4 Flow»

<details close><summary> Задача New Posts </summary>
    <br>
    
В проекте реализован следующий функционал:

1. Посты, загружаемые в фоне (через `getNewer`), не отображаются сразу в `RecyclerView`, вместо этого выводится "плашка" как в [Vk](https://github.com/netology-code/andin-homeworks/blob/master/11_flow/pic/vk.png):
![](pic/vk.png)

![](https://github.com/netology-code/andin-homeworks/blob/master/11_flow/pic/vk.png)

2. При нажатии на "плашку" производится плавный скролл `RecyclerView` к самому верху и отображаются загруженные посты (сама "плашка" после этого удаляется).

</details>

#### Домашнее задание к занятию «4.1. Загрузка и отображение изображений»

<details close><summary> Задача Photo </summary>
    <br>
    
На примере загрузки изображений, реализовано их отображение. В качестве аналога взято приложение ***ВКонтакте***.

Если в посте есть картинка, то она отображается внутри этого поста. Если кликнуть на картинку, она открывается на весь экран:

![](https://github.com/netology-code/andin-homeworks/raw/master/12_images/pic/02.png)

Задача реализована через фрагменты, т.е. при клике на картинку открывается новый фрагмент, на котором изображение выводится на весь экран.

</details>

#### Домашнее задание к занятию «4.2. Регистрация, аутентификация и авторизация»

<details close><summary> Задача Аутентификация </summary>
    <br>
    
При нажатии на пункт меню **«Sign in»** реализована следующая последовательность действий:

1\. Открывается фрагмент с полями для ввода логина и пароля и кнопкой «Войти». Для этого фрагмента создана собственная `ViewModel`.

2\. Происходит отправка запроса пары логин / пароль с получаемым ответом в виде JSON.

3\. Далее сохраняется в `AppAuth`.

</details>

<details close><summary> Sign In to ... и Are you sure?* </summary>
    <br>
    
Реализован следующий функционал:

1\. Когда на экране находится лента постов в `PostViewModel`, проходит проверка, аутентифицирован ли пользователь. Проверка проходит при:
   * добавлении поста (нажатие на `addPost` (+);
   * лайке поста.
      
Если пользователь не аутентифицирован, появляется диалоговое окно с предложением пройти аутентификацию. Пользователь перенаправляется на фрагмент аутентификации.

2\. При создании поста возникает диалоговое окно с подтверждением выхода, если пользователь в `ActionBar` выбрал пункт меню `Sign Out`.

Если пользователь подтвердил выход, то перенаправляется на предыдущий фрагмент.

</details>

<details close><summary> Регистрация* </summary>
    <br>
    
При нажатии на пункт меню **«Sign Up»** реализована следующая последовательность действий:

1\. Открывается фрагмент с 4 полями для ввода имени, логина, пароля и подтверждения пароля и кнопкой «Зарегистрироваться». Для этого фрагмента создана собственная `ViewModel`.

2\. Отправляется запрос и в ответ получен JSON.

3\. Происходит сохранение в `AppAuth`.  
    
</details>

#### Домашнее задание к занятию «4.3. Рассылка и приём push-уведомлений»

<details close><summary> Задача RecipientId </summary>
    <br>
    
Реализована проверка `recipientId` при получении push-уведомления с сервера.

Для тестирования при помощи ***Postman*** отправлялся запрос вида:

```http request
POST http://localhost:9999/api/pushes?token=<--- Used TOKEN is set here --->
Content-Type: application/json
{
  "recipientId": null,
  "content": "Hello !!!"
}
```

</details>
    </details>


*****

<details close><summary> HomeWorkAndAd (Block 3) </summary>
    <br>
    
#### Домашнее задание к занятию «1.1. Dependency Injection»

<details close><summary> Задача Dagger Hilt</summary>
    <br>
    
Призведена миграция проекта на **Dagger Hilt**.

</details>  

<details close><summary> Задача Singletons</summary>
    <br>

В приложении с лекции в `MainActivity` используются следующие конструкции:

```kotlin
FirebaseMessaging.getInstance().token.addOnCompleteListener { task ->
    ...
}
with(GoogleApiAvailability.getInstance()) {
    ...
}
```

Заменены вызовы `getInstance` на ***Dependency Injection***.

</details> 

#### Домашнее задание к занятию «1.3. Architecture Components. Часть 2»

<details close><summary> Задача Refresh on Login/Logout</summary>
    <br>
    
Внесены изменения для реализации запросов с сервера заново при произведении `login/logout`.

</details>  


#### Домашнее задание к занятию «1.2. Architecture Components. Часть 1»

<details close><summary> Задача Refresh to Prepend </summary>
    <br>
    
Произведены следующие изменения:

   - Автоматический PREPEND отключен, т. е. при scroll к первому сверху элементу данные автоматически не подгружаются.
   - REFRESH не затирает предыдущий кеш, а добавляет данные сверху, учитывая ID последнего поста сверху. 
   - APPEND работает в обычном режиме.

</details>

#### Домашнее задание к занятию «1.4. RecyclerView — продвинутое использование»

<details close><summary> Задача Paging Refresh, Prepend & Append </summary>
    <br>
    
Использовав примеры с лекции и [Codelab](https://developer.android.com/codelabs/android-paging), посвящённую Paging, в код проекта добавлена, поддержка PREPEND, APPEND и REFRESH, следующего поведения:

- Refreshing SwipeRefreshLayout отображается только при REFRESH.
- При PREPEND первый элемент в RecyclerView - элемент с загрузкой.
- При APPEND последний элемент в RecyclerView - элемент с загрузкой.

</details>
    </details>


*****

