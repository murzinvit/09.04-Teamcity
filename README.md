## 09.04-Teamcity</br>
#### Подготовка к выполнению
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
#### Основная часть: </br>
1.Создайте новый проект в teamcity на основе fork: </br>
 ![screen](https://github.com/murzinvit/screen/blob/0273c89b0832235d44b64c492c24fbfa8057ba7e/New_progect_create.jpg)
 ![screen](https://github.com/murzinvit/screen/blob/0908e37be5fe544aa445ad079ea90aee7bff578f/Teamcity_VCS_root.jpg)
2.Сделайте autodetect конфигурации: </br>
 ![screen](https://github.com/murzinvit/screen/blob/5340a0c3570d57b804351ed69d4f401b47bef3ec/Teamcity_autodetect_buildsteps.jpg)
3.Сохраните необходимые шаги, запустите первую сборку master'a: </br>
 ![screen](https://github.com/murzinvit/screen/blob/23915ce96b856cb54169526cc000d2d6c675940a/Teamcity_buil_on_master.jpg)
4.Поменяйте условия сборки: если сборка по ветке master, то должен происходит mvn clean package, иначе mvn clean test: </br>
 Для выполнения cделал ветку - dev от master: `git clone git@github.com:murzinvit/example-teamcity.git && git checkout -b "dev" && git push origin dev` </br>
 Создал проект.</br>
 Создал VCS Root из репозитория example-teamcity с default branch - dev</br>
 Создал VCS Root из репозитория example-teamcity с default branch - master</br>
 При создании VCS root, поле - VCS root name уникально и произвольно для каждого VCS root</br>
 В проекте создал 2 BuildStepsConfigurations на каждый VCS Root свою - clean test, clean package шаги соответственно для dev и master</br>
![screen](https://github.com/murzinvit/screen/blob/79f2e714de33777fc2f06b0bdf06d60211dcada1/Teamcity_build_on_branch_dev.jpg)
![screen](https://github.com/murzinvit/screen/blob/d68ae895084e971a2697480809e87e7e821cf03e/Teamcity_build_goals.jpg)
![screen](https://github.com/murzinvit/screen/blob/f6033dfcfb06f5b87124018b5f738f9d44fe3cd3/Build_in_master_branch.jpg)
![screen](https://github.com/murzinvit/screen/blob/fa06bd5041e390e93a6b3827ef1b1b0c27fe9f8c/Teamcity_build_on_master_changes.jpg)
5. Мигрируйте build configuration в репозиторий: </br>
   Добавить Connections на github(в Root_Project) [Инструкция](https://www.jetbrains.com/help/teamcity/configure-and-run-your-first-build.html#Create+project+pointing+to+GitHub.com+repository) </br>
   ![screen](https://github.com/murzinvit/screen/blob/3fc63d017518169500d83d6ea447780dd64a3e6c/Teamcity_build_from_github.jpg)
6. Создайте отдельную ветку feature/add_reply в репозитории: </br>
  `git clone git@github.com:m....`, `git checkout -b "feature/add_reply` </br>
7. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово hunter: </br>
   [Welcomer.java](https://github.com/murzinvit/example-teamcity/blob/feature/add_reply/src/main/java/plaindoll/Welcomer.java) </br>
8. Дополните тест для нового метода на поиск слова hunter в новой реплике: [WelcomerTest.java](https://github.com/murzinvit/example-teamcity/blob/feature/add_reply/src/test/java/plaindoll/WelcomerTest.java)</br>
9. Сделайте push всех изменений в новую ветку в репозиторий: </br>
   `git add -A, git commit -m "Add Hunter", git push origin feature/add_reply`  [feature/add_reply](https://github.com/murzinvit/example-teamcity/tree/feature/add_reply) </br>
10. Убедитесь что сборка самостоятельно запустилась, тесты прошли успешно: </br>
 Добавил новый в Teamcity новый VCS Root c default branch - feature/add_reply </br>
 Добавил триггер при коммите в ветку - запуск buid: </br>
 ![screen](https://github.com/murzinvit/screen/blob/f588710756559a7fd3c908ae8f0d14f7d288707c/Teamcity_trigger.jpg)
 ![screen](https://github.com/murzinvit/screen/blob/dc4aecdf3ca9905e632e25224822a9d6d391f269/Teamcity_build_add_reply.jpg)
11. Внесите изменения из произвольной ветки feature/add_reply в master через Merge: </br>
`git merge feature/add_reply && git push origin master`  [repo_merged](https://github.com/murzinvit/example-teamcity)</br>
12. Убедитесь, что нет собранного артефакта в сборке по ветке master: </br>
 ![screen](https://github.com/murzinvit/screen/blob/fb0b335a713f07189bd89985181e514834469fd1/No_artefacts.jpg)</br>
13. Настройте конфигурацию так, чтобы она собирала .jar в артефакты сборки: </br>
    jar получается из шагов clean и package, указать в build steps:</br>
    Настроить публикацию артифакта можно в Progect -> General Settings -> Artifact paths -> target </br>
    ![screen](https://github.com/murzinvit/screen/blob/811dc8072851fcf0c3512219dab8ce1fcddc9b34/Teamcity_artifact_public.jpg)
14. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны: </br>
   ![screen](https://github.com/murzinvit/screen/blob/40830850752bf9fde5a42b3edf54583e8d96cc08/Teamcity_artifacts_jar.jpg)
15. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity:</br>


### Рабочие заметки:
### Добавить VCS Root in Build Steps:
![screen](https://github.com/murzinvit/screen/blob/493590593f657745f0766cc0a4f2f311eccbc7bf/Teamcity_add_VCS_in_BuildSteps.jpg)
При попытке docker-compose up на virtulbox Ubuntu:
![screen](https://github.com/murzinvit/screen/blob/ba203c3de3f2d5a2e3585d6ef0e6857f277beeb1/Error_in_enviroment_deploy.png)
Cделал ветку - dev от master: git clone git@github.com:murzinvit/example-teamcity.git && git checkout -b "dev" && git push origin dev </br>
Далее создал проект где указал основной веткой - dev, в build steps добавил clean test, добавил триггер при коммите в ветку - запуск buid: </br>
Сделал изменения в pom.xml - version - 0.2.1, groupId - DevOps6, далее закоммитил и запушил изменения: </br>
 Нажать на значке github и авторизоваться выйдет список репозиториев: </br>
![screen](https://github.com/murzinvit/screen/blob/e61843793bf13077bf5d66c17a9387576b60835b/Teamcity_transfer_to_github.jpg)
