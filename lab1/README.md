#Загрузка больших файлов
spring.servlet.multipart.max-file-size=30MB
spring.servlet.multipart.max-request-size=30MB
#mysql.ini
max_allowed_packet = 30M

# контроллер для конвертирования утвержденных техкарт в новую отдельную таблицу
/covertNewArchProject
/covertNewArchProjectJPG

logging.config=log4j2.xml

# Параметры ежедневного резервирования
# каждый день 1:01
cron.expression=0 1 1 * * ?
# необходимо настраивать под систему
cmd-backup=md c:\\backup\\%DATE%\\upload-dir&c:\\wamp\\bin\\mysql\\mysql5.6.12\\bin\\mysqldump -uroot --databases karta > c:\\backup\\%DATE%\\dump.sql&copy /Y upload-dir c:\\backup\\%DATE%\\upload-dir
cmd-clear=rd /s /q c:\\backup\\%DATE%
# для Linux
cmd-backup-linux=mkdir -p backup/%DATE%/upload-dir;mysqldump -uroot -pAa1234 --databases karta > backup/%DATE%/dump.sql;cp -p upload-dir backup/%DATE%/upload-dir
cmd-clear-linux=rm -r backup/%DATE%

# Параметры почты

spring.mail.host=10.1.32.3
spring.mail.username=d_server
spring.mail.password=Sa1532
spring.mail.port=25
spring.mail.protocol=smtp

# Для запуска приложения необходимо, чтобы:
***
На компьютере был установлен MySQL

# Далее нужно создать пустую базу данных

# Затем изменить файл application.properties:

## Сделать изменения в строке
***
spring.datasource.url=jdbc:mysql://localhost:3306/train_reg
## Например, на такие:
***
spring.datasource.url=jdbc:mysql://localhost:3306/example
- где example - имя созданной базы данных 
- а 3306 - номер порта, используемого MySQL

## Также нужно изменить строчки
***
>spring.datasource.username=springuser  
spring.datasource.password=ThePassword  

> Необходимо вписать логин и пароль своего пользователя MySQL
# После запуска проекта дописываем в адресной строке браузера /registration
***
Заполнив форму логин\пароль, добавим пользователя в БД по нажатию на кнопку,  
теперь можно вернуться на страницу авторизации и войти по только что  
добавленному логину и паролю

***
Как добавить пользователя с ролью Админ?
***
В 51-ой строке файла RegistrationController
>user.setRoles(Collections.singleton(Role.USER)); 
>заменяем Role.USER на Role.ADMIN
>перезапускаем проект, переходим в /registration
>добавляем пользователя с любым логином и паролем и он будет обладать ролью Админа, входим в систему под его логином и получаем доступ к UserList'у