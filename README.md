## 09.04-Teamcity</br>
1. Поднимите инфраструктуру teamcity</br>
Поднял так: </br>
    Docker pull jetbrains/teamcity-server:latest && Docker run -d -p 8111:8111 --name team-srv jetbrains/teamcity-server:latest </br>
    После стандартных настроек, во вкладке - Agents push указал ip + login/password машины в роли агента(без агентов билды не работают) </br>
Либо так: </br>
Ставим docker-compose: `apt-get update && apt install docker-compose -y` </br>
Клонируем репозиторий: `git clone https://github.com/netology-code/mnt-homeworks.git` </br>
Для поднятия инфраструктуры свободного места на диске нужно более 10Gb, т.к контейнеры по 2.2Gb: `cd / && df -h` </br> 
Выполняем: `cd ./mnt-homeworks/09-ci-04-teamcity/teamcity && docker-compose up` </br> 
5. Сделайте fork репозитория [aragastmatb/example-teamcity](https://github.com/aragastmatb/example-teamcity) Форк: [https://github.com/murzinvit/example-teamcity](https://github.com/murzinvit/example-teamcity) </br>
Далее сделал ветку dev от master: git clone git@github.com:murzinvit/example-teamcity.git && git checkout -b "dev" && git push origin dev </br>  

### Заметки:
При попытке docker-compose up на virtulbox Ubuntu:
![screen](https://github.com/murzinvit/screen/blob/ba203c3de3f2d5a2e3585d6ef0e6857f277beeb1/Error_in_enviroment_deploy.png)
