## 09.04-Teamcity</br>
1. Поднимите инфраструктуру teamcity</br>
> Ставим docker-compose: `apt-get update && apt install docker-compose -y` </br>
> Клонируем репозиторий: `git clone https://github.com/netology-code/mnt-homeworks.git` </br>
> Для поднятия инфраструктуры свободного места на диске нужно более 10Gb, т.к контейнеры по 2.2Gb: `cd / && df -h` </br> 
> Выполняем: `cd ./mnt-homeworks/09-ci-04-teamcity/teamcity && docker-compose up` </br> 

2. Если хочется, можете создать свою собственную инфраструктуру на основе той технологии, которая нравится. Инструкция по установке из документации </br>
3. Дождитесь запуска teamcity, выполните первоначальную настройку </br>
4. Авторизуйте агент </br>
5. Сделайте fork репозитория [aragastmatb/example-teamcity](https://github.com/aragastmatb/example-teamcity): </br>
> Форк: [https://github.com/murzinvit/example-teamcity](https://github.com/murzinvit/example-teamcity) </br>

### Заметки:
При попытке docker-compose up на virtulbox Ubuntu:
![screen](https://github.com/murzinvit/screen/blob/ba203c3de3f2d5a2e3585d6ef0e6857f277beeb1/Error_in_enviroment_deploy.png)
