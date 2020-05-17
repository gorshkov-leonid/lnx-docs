* Действия
  * Отключение Defender
  * Изменение параметров электропитания
    * В режиме администратора `powercfg -h off`
    * Панель управления -> Оборудование и звук -> Электропитание
      * Дополнительные схемы -> Высокая Производительность -> Выбрать -> Настройка схемы электропитания
        * (опционально) Настройка отключения дисплея -> Никогда   
        * Изменить дополнительные параметры
          * Отключать жесткий диск через -> 0 мин
          * Сон -> Сон после -> Никогда
          * Гибернация -> Гибернация после -> Никогда     
      * (левая панель) Действие кнопок питания (системные параметры)
        * Действия не требуются
        * Включить быстрый запуск -> Disabled
  * Активация 
  * Первоначальная настройка отображения
    * Разрешение экрана
    * Мелкие значи на столе
    * Персонализация -> Темы -> Параметры значков рабочего стола
    * Персонализация -> Пуск -> "Выбирете, какие папки будут отображаться в меню Пуск"
  * Перенос данных Windows на другой диск
    * /Users    
      * /Users/me/AppData/Local/Packages
      * /Users/me/Public
    * /hyberfil.sys (удалится при настройке питания)
    * /pagefile.sys, /swapfile.sys 
      * Система -> Дополнительные параметры -> Быстродействие: Параметры -> Дополнительно -> Вируальная память: Изменить -> Выбрать диск и снять размеры
      * Для тонкой настройки статья: [Зачем нужен файл swapfile.sys](https://zen.yandex.ru/media/id/5a3211a177d0e6afcba2adfd/zachem-nujen-fail-swapfilesys-v-windows-10-i-mojno-li-ego-udalit-5b5041479b38ef00a9d98170)
    * /System Volume Information
    * /PerfLogs    
    * /Recovery
    * /Windows/WinSxS    
  * Установка программ
  
* Список моих программ
  * Kaspersky
  * Microsof Office
  * Google Chrome / Firefox
  * Cisco AnyConnect
  * Remote Desktop
  * Intellij Idea
  * Docker
  * WSL(1/2)
  * Total Commander
  * Notepad++ 
  
* Полезные утилиты
  * [Tree Size](https://www.jam-software.com/treesize_free)
  * [Light Shot](https://app.prntscr.com/ru/index.html)
  * [7zip](https://www.7-zip.org/download.html)

* TMP
  * [Как переместить папку Пользователи (Users) на другой диск в Windows 10](http://www.oszone.net/27689/windows_10_relocate_users_folder)
  * [Как перенести профиль пользователя на другой диск?](https://answers.microsoft.com/ru-ru/windows/forum/windows_10-security/%D0%BA%D0%B0%D0%BA/b15edd96-8596-41fa-8221-1acb6fafb009?auth=1)
  * http://www.outsidethebox.ms/17670/
