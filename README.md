# Основы Git - Работа с удалёнными репозиториями

## Работа с удалёнными репозиториями

Для того, чтобы внести вклад в какой-либо Git-проект, вам необходимо уметь работать с удалёнными репозиториями. Удалённые репозитории представляют собой версии вашего проекта, сохранённые в интернете или ещё где-то в сети. У вас может быть несколько удалённых репозиториев, каждый из которых может быть доступен для чтения или для чтения-записи. Взаимодействие с другими пользователями предполагает управление удалёнными репозиториями, а также отправку и получение данных из них. Управление репозиториями включает в себя как умение добавлять новые, так и умение удалять устаревшие репозитории, а также умение управлять различными удалёнными ветками, объявлять их отслеживаемыми или нет и так далее. В данном разделе мы рассмотрим некоторые из этих навыков.

*Примечание:
Удалённый репозиторий может находиться на вашем локальном компьютере.
Вполне возможно, что удалённый репозиторий будет находиться на том же компьютере, на котором работаете вы. Слово «удалённый» не означает, что репозиторий обязательно должен быть где-то в сети или Интернет, а значит только — где-то ещё. Работа с таким удалённым репозиторием подразумевает выполнение стандартных операций отправки и получения, как и с любым другим удалённым репозиторием.*

## Просмотр удалённых репозиториев

Для того, чтобы просмотреть список настроенных удалённых репозиториев, вы можете запустить команду git remote. Она выведет названия доступных удалённых репозиториев. Если вы клонировали репозиторий, то увидите как минимум origin — имя по умолчанию, которое Git даёт серверу, с которого производилось клонирование:

Вы можете также указать ключ -v, чтобы просмотреть адреса для чтения и записи, привязанные к репозиторию:

$ git remote -v

## Добавление удалённых репозиториев

В предыдущих разделах мы уже упоминали и приводили примеры добавления удалённых репозиториев, сейчас рассмотрим эту операцию подробнее. Для того, чтобы добавить удалённый репозиторий и присвоить ему имя (shortname), просто выполните команду git remote add (shortname) (url):

## Получение изменений из удалённого репозитория — Fetch и Pull

Как вы только что узнали, для получения данных из удалённых проектов, следует выполнить:

$ git fetch [remote-name]

Данная команда связывается с указанным удалённым проектом и забирает все те данные проекта, которых у вас ещё нет. После того как вы выполнили команду, у вас должны появиться ссылки на все ветки из этого удалённого проекта, которые вы можете просмотреть или слить в любой момент.

Когда вы клонируете репозиторий, команда clone автоматически добавляет этот удалённый репозиторий под именем «origin». Таким образом, git fetch origin извлекает все наработки, отправленные на этот сервер после того, как вы его клонировали (или получили изменения с помощью fetch). Важно отметить, что команда git fetch забирает данные в ваш локальный репозиторий, но не сливает их с какими-либо вашими наработками и не модифицирует то, над чем вы работаете в данный момент. Вам необходимо вручную слить эти данные с вашими, когда вы будете готовы.

Если ветка настроена на отслеживание удалённой ветки , то вы можете использовать команду git pull чтобы автоматически получить изменения из удалённой ветки и слить их со своей текущей. Этот способ может для вас оказаться более простым или более удобным. К тому же, по умолчанию команда git clone автоматически настраивает вашу локальную ветку master на отслеживание удалённой ветки master на сервере, с которого вы клонировали репозиторий. Название веток может быть другим и зависит от ветки по умолчанию на сервере. Выполнение git pull, как правило, извлекает (fetch) данные с сервера, с которого вы изначально клонировали, и автоматически пытается слить (merge) их с кодом, над которым вы в данный момент работаете.

*Примечание:
Начиная с версии 2.27, команда git pull выдаёт предупреждение, если настройка pull.rebase не установлена. Git будет выводить это предупреждение каждый раз пока настройка не будет установлена.*

*Если хотите использовать поведение Git по умолчанию (простое смещение вперёд если возможно — иначе создание коммита слияния): git config --global pull.rebase "false"*

*Если хотите использовать перебазирование при получении изменений: git config --global pull.rebase "true".*

## Отправка изменений в удалённый репозиторий (Push)

Когда вы хотите поделиться своими наработками, вам необходимо отправить их в удалённый репозиторий. Команда для этого действия простая: git push. Чтобы отправить вашу ветку master на сервер origin (повторимся, что клонирование обычно настраивает оба этих имени автоматически), вы можете выполнить следующую команду для отправки ваших коммитов:

$ git push origin master

Эта команда срабатывает только в случае, если вы клонировали с сервера, на котором у вас есть права на запись, и если никто другой с тех пор не выполнял команду push. Если вы и кто-то ещё одновременно клонируете, затем он выполняет команду push, а после него выполнить команду push попытаетесь вы, то ваш push точно будет отклонён. Вам придётся сначала получить изменения и объединить их с вашими и только после этого вам будет позволено выполнить push. 

## Просмотр удалённого репозитория

Если хотите получить побольше информации об одном из удалённых репозиториев, вы можете использовать команду git remote show.

Данная команда показывает какая именно локальная ветка будет отправлена на удалённый сервер по умолчанию при выполнении git push. Она также показывает, каких веток с удалённого сервера у вас ещё нет, какие ветки всё ещё есть у вас, но уже удалены на сервере, и для нескольких веток показано, какие удалённые ветки будут в них влиты при выполнении git pull.

## Удаление и переименование удалённых репозиториев

Для переименования удалённого репозитория можно выполнить git remote rename. Например, если вы хотите переименовать pb в paul, вы можете это сделать при помощи git remote rename:

$ git remote rename pb paul

$ git remote

origin

paul

Стоит упомянуть, что это также изменит имена удалённых веток в вашем репозитории. То, к чему вы обращались как pb/master, теперь стало paul/master.

Если по какой-то причине вы хотите удалить удалённый репозиторий — вы сменили сервер или больше не используете определённое зеркало, или кто-то перестал вносить изменения — вы можете использовать git remote rm:

$ git remote remove paul

$ git remote

origin

При удалении ссылки на удалённый репозиторий все отслеживаемые ветки и настройки, связанные с этим репозиторием, так же будут удалены.


## Отключение удаленного репозитория от локального (команда git remote remove).

git remote remove <название удаленного репозитория> отключает переданный удаленный репозиторий от вашего.


## Работа с репозиторием, создание форков и пулл-реквестов

Прежде всего вам необходимо зарегистрироваться на GitHub,  После регистрации вы попадете на главную страницу. На ней будут отображаться действия людей, на которых вы подписались и обновления в репозиториях, которые вы добавили в избранное.

Чтобы создать свой репозиторий, нажмите на зеленую кнопку New.
Перед вами откроется страница создания репозитория. Давайте разберем, что за поля нам предлагают заполнить.

Итак, первое поле Repository name – имя репозитория.
Второе поле – Description – описание. Его заполнять необязательно. Но другим пользователям, которые попали на страницу вашего репозитория, будет проще понять, что перед ними, если вы заполните графу описания.
Затем вы можете выбрать, будет ли репозиторий открытым, то есть доступным абсолютно всем пользователям GitHub, или закрытым, то есть доступным только вам и людям, которым вы предоставите доступ.
Последние три поля предлагают нам добавить, соответственно, README-файл, .gitignore файл и выбрать лицензию для нашего проекта.
GitHub автоматически создал первый коммит, добавив в него файл .gitignore и файл README.
Кстати, можно заметить, что содержимое файла README выводится под рабочей копией репозитория. Это одна из особенностей GitHub. Вы в любое время можете создать файл с именем README.md и запушить его в свой удаленный репозиторий на GitHub. Тогда содержимое этого файла будет отображаться прямо на странице вашего репозитория.
1. Вкладка Code. В ней содержится рабочая копия нашего репозитория (по центру), описание (справа), вывод файла README (под рабочей копией), история коммитов, а также кнопки для клонирования репозитория и просмотра файлов.
2. Вкладка Issues. В этой вкладке будут отображаться все запросы, сделанные другими пользователями. Как правило, пользователи используют запрос, чтобы сообщить о найденном баге, либо чтобы задать какой-то вопрос о вашем приложении.
3. Вкладка Pull-requests. На этой вкладке будут отображаться все пулл-реквесты, сделанные другими пользователями. 
4-5. Вкладки Actions и Project относятся скорее к системе CI/CDI, которую предоставляет GitHub, в этом курсе мы не будем затрагивать их.
6. Вкладка Wiki открывает вам доступ к созданию и размещению документации о собственном проекте.
7. На вкладке Security содержатся различные настройки безопасности вашего проекта. Там же можно включить инспекцию вашего кода, чтобы узнать, если вы случайно загрузите какой-нибудь секретный токен на GitHub.
8. Вкладка Insight содержит различную информацию и статистические данные об активности репозитория. Там вы сможете посмотреть на зависимость количества коммитов в репозитории от времени или на процент коммитов, сделанных вами.
9. Последняя вкладка – Settings. В ней находятся различные настройки вашего репозитория. Там вы можете поменять видимость репозитория, сделав его частным, или вовсе удалить репозиторий.

## Создание форка репозитория на GitHub. Пулл-реквесты.

1. Для начала зайдем на страницу репозитория проекта. Нажимаем на кнопку Fork,  После этого Git создаст точную копию этого репозитория в вашем аккаунте.
2. Клонируем репозиторий к себе на компьютер командой git clone. Создадим файл README.md с описанием проекта, чтобы другим пользователям было понятно, в чем отличие этой реализации от остальных.

3. Сделаем коммит и выполним git push, чтобы загрузить наши изменения в удаленный репозиторий.

4. Теперь GitHub подсказывает нам, что наша ветка опережает ветку исходного репозитория на один коммит и предлагает сделать пулл-реквест.
5. Нажимаем на кнопку Compare на подсказке GitHub, либо переходим на вкладку Pull Requests и нажимаем New pull request.
6. Перед нами откроется страница создания пулл-реквеста.
Здесь мы можем просмотреть внесенные изменения и выбрать две ветки: одну в исходном репозитории, на нее будут залиты наши изменения, вторую – в нашем репозитории, с нее будут скачаны изменения. Как только мы выбрали ветки и убедились, что не внесли никаких лишних изменений, нажимаем кнопку Create pull request.
Здесь необходимо описать, что за изменения вы внесли и почему они были необходимы. Сообщение, которое оставили мы, видно на картинке. Оно отражает суть и необходимость внесенных изменений. Как только мы закончили с описанием, можно нажимать кнопку Create pull request.

8. Теперь мы попадаем на страницу уже созданного пулл-реквеста в изначальном репозитоии. 
Именно так будет выглядеть наш пулл-реквест и для владельца репозитория. На этой странице он сможет писать комментарии, указывая на ошибки или задавая вопросы. После того, как владелец репозитория просмотрит наши изменения и убедится, что они не имеют вредоносный характер, он сможет принять наш пулл-реквест. Тогда все изменения, добавленные в этот пулл-реквест нами, будут залиты в исходный репозиторий.