## Отчет о выполнении тестового задания ООО "Муниципальные решения"
Исполнитель Михаил Тимофеев

### Задание реализуется в среде:
- openSUSE Leap 42.3;
- nodejs6 6.14.1-9.2, postgresql96-server, git,... из системного репозитария;
- Sails v0.12.14

## Техническое задание на разработку
### Функциональные требования и их реализация

1. На главной странице указать имя и фамилию разработчика<br>
- исправлен ./views/homepage.jade<br><br>

2. Исправить ошибку. Авторизация нового пользователя происходит независимо от того подтвержден email пользователя или нет. Если пользователь не активирован (не подтвержден его email), то система не должна его пускать, выводя соответствующее сообщение и ссылку для отправки повторного email со ссылкой активации. (*Подсказка. Это можно реализовать с помощью [политик доступа sails.js](http://sailsjs.org/documentation/concepts/policies)*)<br><br>
- исправлена ошибка: cервер Sails падает при попытке входа незарегистрированного пользователя:<br>
/home/miktim/Private/sails/cloudmaps_test/api/controllers/UserController.js:82
          if(user.password == crypto.createHash('sha256').update(req.param('password')).digest('hex')){
                 ^
TypeError: Cannot read property 'password' of undefined
- исправлен UserController.js:
  - метод login - в соответствии с требованиями;
  - отсылка сообщения активации (POST) и активация (GET) объединены в один метод activatе;
  - метод register вызывает метод activate (POST) для отсылки сообщения активации;
  - в списке запросов в друзья исключены неактивированные пользователи;
- дополненны  polices.js, routes.js;
- добавлен send_activation.jade.
<br><br>

3. Исправить искажение аватарки при отображении в списке пользователей, если исходная картинка не является квадратной. Решение проблемы желательно сделать средствами plupload. (*Подсказка. Сейчас средствами plupload делается масштабирование изображения перед загрузкой*)<br>
- в profile.jade для plupload установлено свойство масштабирования crop: true (thumbnail)<br><br>

4. Создать и добавить к проекту favicon.<br>
- решение со stackowerflow и, вроде, работает:
  - файл favicon.png размещен в каталоге /assets ;
  - изменен layout.jade.<br><br

5. Добавить информацию о том, кто из пользователей в данный момент online в списке друзей, запросов в друзья и списке пользователей при поиске новых друзей. Постараться реализовать изменение статуса пользователя без необходимости перегружать страницу в браузере. Сейчас так реализована отправка запроса в друзья, подтверждение и отклонение запроса в друзья. (*Подсказка. Использовать [предоставляемые sails.js средства работы с web-сокетами](http://sailsjs.org/documentation/reference/web-sockets)*).
- 
<br><br><br><br>
### Не реализовано
6. Если пользователь online, то при просмотре его профиля другим пользователем он должен видеть на карте место положения того пользователя, профиль которого в данный момент просматривается. Если пользователь offline, то отображать на карте точку его последнего пребывания. Должно быть понятно, что в данный момент отображается на карте: текущее положение или предыдущее положение пользователя. Если же по каким-то причинам не возможно установить текущее или предыдущее положения пользоввателя (например. пользователь не дал разрешение на определение его положения при запросе в браузере), то это тоже должно быть понятно. Способ реализации функционала определяет разработчик.
7. Изменить url профиля пользователя с user/\<id\> на user/\<username\>
8. Реализовать просмотр профилей друзей из списка. При попытке просмотреть профиль пользователя, не являющегося другом, путем явного указания url его профиля, необходимо выводить сообщение о невозможности просмотра данной информации.
9. Реализовать обмен сообщениями между друзьями. Глубина проработки этого функционала остается на усмотрение разработчика и зависит от возможностей и временнЫх ресурсов.


