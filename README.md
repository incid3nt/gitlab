# Домашнее задание к занятию "`GITLAB`" - `Еноктаев Олег`


### Инструкция по выполнению домашнего задания

  
---

### Задание 1

Что нужно сделать:

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в этом [репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.
В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

---
1.1 Разворачиваем GITLAB локально:
Обновим пакеты:
```
sudo apt update
sudo apt upgrade
```
Установим зависимости, которые необходимы для работы:
```
sudo apt install -y curl ssh openssh-server ca-certificates tzdata perl
```
Перейдите в директорию tmp:
```
cd \tmp
```
Затем загрузим в нее скрипт установки:
```
curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh

```
запускаем скрипт:
```
sudo bash /tmp/script.deb.sh
```
Установим GITLAB
```
sudo apt install gitlab-ce
```
Настроим конфиг.файл:
```
sudo nano /etc/gitlab/gitlab.rb
```
В строке external_url укажем наш IP адрес для gitlab:
```
external_url ‘http://192.168.1.23’
```
Обновим конфигурацию:
```
sudo gitlab-ctl reconfigure
```
Gitlab установлен

![служба](https://github.com/incid3nt/gitlab/blob/main/screen/putty_8yLs8pIumF.png)

![браузер](https://github.com/incid3nt/gitlab/blob/main/screen/chrome_ewTHKGtmFK.png)
---
1.2 Создайте новый проект и пустой репозиторий в нём.
![Репозиторий](https://github.com/incid3nt/gitlab/blob/main/screen/chrome_oRq4LZiU0g.png)
![Репозиторий](https://github.com/incid3nt/gitlab/blob/main/screen/chrome_pqkO34xCxE.png)
---
1.3 Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.
Регистрация раннера:
```bash
   docker run -ti --rm --name gitlab-runner \
     --network host \
     -v /srv/gitlab-runner/config:/etc/gitlab-runner \
     -v /var/run/docker.sock:/var/run/docker.sock \
     gitlab/gitlab-runner:latest register
```
Конфигурация раннера для docker-in-docker:
```yaml
    volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock"]
    extra_hosts = ["gitlab.localdomain:192.168.56.10"]
```
Запуск:
```bash
   docker run -d --name gitlab-runner --restart always \
     --network host \
     -v /srv/gitlab-runner/config:/etc/gitlab-runner \
     -v /var/run/docker.sock:/var/run/docker.sock \
     gitlab/gitlab-runner:latest
```
--- 
```bash
root@gitlab:/srv/gitlab-runner/config# docker run -ti --rm --name gitlab-runner \
     --network host \
     -v /srv/gitlab-runner/config:/etc/gitlab-runner \
     -v /var/run/docker.sock:/var/run/docker.sock \
     gitlab/gitlab-runner:latest register
Runtime platform                                    arch=amd64 os=linux pid=7 revision=3153ccc6 version=17.7.0
Running in system-mode.

Enter the GitLab instance URL (for example, https://gitlab.com/):
http://192.168.1.23
Enter the registration token:
GR1348941K6ZpP-65VhQDe_Lfhr1E
Enter a description for the runner:
[gitlab]:
Enter tags for the runner (comma-separated):
yandex
Enter optional maintenance note for the runner:

WARNING: Support for registration tokens and runner parameters in the 'register' command has been deprecated in GitLab Runner 15.6 and will be replaced with support for authentication tokens. For more information, see https://docs.gitlab.com/ee/ci/runners/new_creation_workflow
Registering runner... succeeded                     runner=GR1348941K6ZpP-65
Enter an executor: ssh, virtualbox, docker, docker-windows, docker-autoscaler, instance, custom, shell, parallels, docker+machine, kubernetes:
docker
Enter the default Docker image (for example, ruby:2.7):
golang:1.17
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!

Configuration (with the authentication token) was saved in "/etc/gitlab-runner/config.toml"
root@gitlab:/srv/gitlab-runner/config# docker run -d --name gitlab-runner --restart always \
     --network host \
     -v /srv/gitlab-runner/config:/etc/gitlab-runner \
     -v /var/run/docker.sock:/var/run/docker.sock \
     gitlab/gitlab-runner:latest
0206a87a1402ed6e6cef72c2bd02b8a1746164342759258595a253e90c7c82fd
```
---
![runner](https://github.com/incid3nt/gitlab/blob/main/screen/chrome_znjKIBHSUp.png)
---
### Задание 2

`Что нужно сделать:`

1. Запушьте репозиторий на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

- В качестве ответа в шаблон с решением добавьте:
- файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне;
- скриншоты с успешно собранными сборками.
---
```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
