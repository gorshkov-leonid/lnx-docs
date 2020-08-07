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
    * /Windows/WinSxS  
    * /Users    
      * /Users/me/AppData/Local/Packages
      * /Users/Public
    * /hyberfil.sys (удалится при настройке питания)
    * /pagefile.sys, /swapfile.sys 
      * Система -> Дополнительные параметры -> Быстродействие: Параметры -> Дополнительно -> Вируальная память: Изменить -> Выбрать диск и снять размеры
      * Для тонкой настройки статья: [Зачем нужен файл swapfile.sys](https://zen.yandex.ru/media/id/5a3211a177d0e6afcba2adfd/zachem-nujen-fail-swapfilesys-v-windows-10-i-mojno-li-ego-udalit-5b5041479b38ef00a9d98170)
    * /System Volume Information
    * /Recovery
    * /Intel/Logs/*
      * Чтобы удалить, нужно отключить службу `cphs` (`Intel(R) Content Protection HECI Service`, программа `C:\Windows\SysWow64\IntelCpHeciSvc.exe`)
      * Описание ``` 
      Embedded in a number of computers with Intel chips starting with second generation core processors.  This file is part of "Intel Insider" and is involved in communication with something concerning content protection.  This program is centered primarily on HDMI films etc.  If you do not view such DRM protected content,  you can disable this service.
      ```       
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

* WSL
   * Enable WSL2 (https://aka.ms/wsl2): 
      1. Requirements: Windows 10 2004 build 19041 or higher
      1. Open console under Admin
      1. `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
      1. `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
      1. `wsl --set-default-version 2`
      1. Restart
      1. Update kernel: https://aka.ms/wsl2kernel  
      1. Relogin
   * Ubuntu WSL
      1. Winows Store -> (Search...) -> Ubuntu  
         1. If error `0x80073D05` occured then open `%localappdata%` and `Packages` in it, futher rename folder that looks like  `CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc`
         1. Alternative way here: https://wiki.ubuntu.com/WSL
      1. Check that Ubuntu installed under WSL2
         1. `wsl --list --verbose`
         1. Expected output:
         ```
           NAME                   STATE           VERSION
           Ubuntu                 Running         2
         ```    
      1. Run Ubuntu, wait installation to be finished then specify username and password
      1. Get fresh updates: `sudo apt update`
   * Docker under WSL
      1. https://get.docker.com/
      1. Relogin
      1. Setup for WSL (https://docs.docker.com/docker-for-windows/wsl/)
         1. Enable Ubuntu here `Settings > Resources > WSL Integration`

   * Links 
      1. https://aka.ms/wsl2
      1. https://aka.ms/wsl2kernel 
      1. https://docs.docker.com/docker-for-windows/wsl/
      1. https://ubuntu.com/blog/ubuntu-on-wsl-2-is-generally-available  

* Полезные утилиты
  * [IObit Unlocker](https://ru.iobit.com/iobit-unlocker.php)
  * [Tree Size](https://www.jam-software.com/treesize_free)
  * [Light Shot](https://app.prntscr.com/ru/index.html)
  * [7zip](https://www.7-zip.org/download.html)
  * [Minitool Partition Wizard](https://www.partitionwizard.com/) - для разбивки дисков, бесплатная бесполезная, сразу ищем полнофункциональную

* TMP
  * [Как переместить папку Пользователи (Users) на другой диск в Windows 10](http://www.oszone.net/27689/windows_10_relocate_users_folder)
  * [Как перенести профиль пользователя на другой диск?](https://answers.microsoft.com/ru-ru/windows/forum/windows_10-security/%D0%BA%D0%B0%D0%BA/b15edd96-8596-41fa-8221-1acb6fafb009?auth=1)
  * http://www.outsidethebox.ms/17670/
