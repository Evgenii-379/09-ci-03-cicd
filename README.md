# **Домашнее задание к занятию 9 «Процессы CI/CD»**-***Вуколов Евгений***
## **Подготовка к выполнению**
1. Создайте два VM в Yandex Cloud с параметрами: 2CPU 4RAM Centos7 (остальное по минимальным требованиям).
2. Пропишите в inventory playbook созданные хосты.
3. Добавьте в files файл со своим публичным ключом (id_rsa.pub). Если ключ называется иначе — найдите таску в плейбуке, которая использует id_rsa.pub имя, и исправьте на своё.
4. Запустите playbook, ожидайте успешного завершения.
5. Проверьте готовность SonarQube через браузер.
6. Зайдите под admin\admin, поменяйте пароль на свой.
7. Проверьте готовность Nexus через бразуер.
8. Подключитесь под admin\admin123, поменяйте пароль, сохраните анонимный доступ.
## **Знакомоство с SonarQube**
### **Основная часть**
1. Создайте новый проект, название произвольное.
2. Скачайте пакет sonar-scanner, который вам предлагает скачать SonarQube.
3. Сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
4. Проверьте sonar-scanner --version.
5. Запустите анализатор против кода из директории example с дополнительным ключом -Dsonar.coverage.exclusions=fail.py.
6. Посмотрите результат в интерфейсе.
7. Исправьте ошибки, которые он выявил, включая warnings.
8. Запустите анализатор повторно — проверьте, что QG пройдены успешно.
9. Сделайте скриншот успешного прохождения анализа, приложите к решению ДЗ.
## **Знакомство с Nexus**
### **Основная часть**
1. В репозиторий maven-public загрузите артефакт с GAV-параметрами:
- groupId: netology;
- artifactId: java;
- version: 8_282;
- classifier: distrib;
- type: tar.gz.
2. В него же загрузите такой же артефакт, но с version: 8_102.
3. Проверьте, что все файлы загрузились успешно.
4. В ответе пришлите файл maven-metadata.xml для этого артефекта.
## **Знакомство с Maven**
### **Подготовка к выполнению**
1. Скачайте дистрибутив с maven.
2. Разархивируйте, сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
3. Удалите из apache-maven-<version>/conf/settings.xml упоминание о правиле, отвергающем HTTP- соединение — раздел mirrors —> id: my-repository-http-unblocker.
4. Проверьте mvn --version.
5. Заберите директорию mvn с pom.
### **Основная часть**
1. Поменяйте в pom.xml блок с зависимостями под ваш артефакт из первого пункта задания для Nexus (java с версией 8_282).
2. Запустите команду mvn package в директории с pom.xml, ожидайте успешного окончания.
3. Проверьте директорию ~/.m2/repository/, найдите ваш артефакт.
4. В ответе пришлите исправленный файл pom.xml.
### **Как оформить решение задания**
Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории

# **Решение**

- Создал виртуальную машину Debian 11 в yandex cloud
При помощи docker-compose установил на Debian 11 SonarQube, Nexus
docker-compose.yml: 

- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-17%20231421.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-17%20231434.png)

- sonar-scanner:
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-18%20235849.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-18%20235859.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-18%20235946.png)

- Сгенерирован проект в каталоге: 
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-19%20210513.png)

- Построен проект командой maven-package:
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20210116.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20210135.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20210147.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20210209.png)
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20213410.png)

- каталоги ~/.m2: 
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20214948.png)

- каталоги java.tar.gz:
- ![scrin](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/Снимок%20экрана%202025-01-23%20215333.png) 


1. [pom.xml](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/pom.xml)
2. [maven-metadata.xml 1](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/maven-metadata.xml%20%20%201)
3. [maven-metadata.xml 2](https://github.com/Evgenii-379/09-ci-03-cicd/blob/main/maven-metadata.xml%20%202)















