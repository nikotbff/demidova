# Demidova

Задача выглядит вот так:

![image](https://github.com/user-attachments/assets/5902559a-27c1-4969-959d-a8b947d8fda4)

Перед началом работы, устанавливаем Linux Oracle на VirtualBox,со следующими параметрами: 2 ядра, 4096 МБ оперативной памяти, а также при установке выбран английский язык.

Далее устанавливаем утилиту wget для скачивания файлов из интернета при помощи команды.

1. `sudo yum install wget`

![image (2)](https://github.com/user-attachments/assets/cca2ec32-d2fd-459d-8d00-d37496f2a3d4)

Далее нужна установка утилиты curl (тут она уже установлена, а данной командой выполняется проверка этого)

2. `sudo yum install curl`

![image](https://github.com/user-attachments/assets/9fce544a-fb43-42a7-ac06-81742c7d9079)

После этого идет команда, которая добавляет репозиторий Docker в список доступных репозиториев для yum, что позволяет далее установить Docker.

3. `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

![image](https://github.com/user-attachments/assets/b2af44c8-a61a-46d6-bcd5-d58b22cad257)

Следующим шагом будет использование команды, которая устанавливает необходимые компоненты Docker

4. `sudo yum install docker-ce docker-ce-cli containerd.io`

![image](https://github.com/user-attachments/assets/032f30f4-2e6f-47f0-9a79-f82ba71c9575)
![image](https://github.com/user-attachments/assets/aa7a54b3-94db-4999-bcda-8d0a6ea75fb0)

Далее запускается команда, которая выполняет две функции: включает Docker для автоматического запуска при каждой загрузке системы, а также немедленно запускает службу Docker.

5. `sudo systemctl enable docker --now`

![image](https://github.com/user-attachments/assets/2906918a-fc99-4f3a-8c01-b3adab185567)

После выполнении команды, переменная COMVER будет содержать версию последнего релиза Docker Compose.

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![image](https://github.com/user-attachments/assets/8044af84-2068-4e18-be49-b34e28253b1e)

После выполнения данной команды, исполняемый файл Docker Compose будет доступен для запуска.

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/8bb379f1-60b2-47df-8c82-e2afbaf0eaf0)

Последующая команда предоставляет права на выполнение файлу /usr/bin/docker-compose, а так же выполняется команда, выволящая на экран информацию о версии установленного Docker Compose.

8. `sudo chmod +x /usr/bin/docker-compose`
9. `docker-compose --version`

![image](https://github.com/user-attachments/assets/5f732e5a-d27c-4faf-aff2-7b59ff336b07)

Следующим шагом скачиваются все файлы и историю изменений из репозитория git.

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/8970a322-b207-4387-9bc7-87cf9f13c832)


При выполнении команды выдается ошибка, исправляемая командой sudo yum install git, позволяющей установить пакеты git.

![image](https://github.com/user-attachments/assets/9e340488-bd04-4e26-977b-91b8b54d3217)

После этого все выполняется корректно.

![image](https://github.com/user-attachments/assets/5a2b17eb-9497-4a4d-a744-e0a4ad01a4c7)

Далее используется утилита cd (change directory) для смены текущего рабочего каталога в командной строке Linux, после чего выполняется ряд команд.

11. `cd grafana_stack_for_docker`

Эта команда использует утилиту mkdir для создания каталогов "директорий" на файловой системе.

12. `sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

Эта команда использует утилиту mkdir с опцией -p и расширением фигурных скобок "brace expansion" для создания нескольких каталогов в файловой системе.

13. `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`
Эта команда использует утилиту chown для изменения владельца "owner" и группы "group" файлов и каталогов.

14. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

Эта команда использует утилиту touch для создания пустого файла.

15. `touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

Эта команда использует утилиту cp "copy" для копирования файлов.

16. `cp config/* /mnt/common_volume/swarm/grafana/config/`

Эта команда использует утилиту mv "move" для переименования файла, обычно приводя имя файла к стандартному или ожидаемому.

17. `mv grafana.yaml docker-compose.yaml`

Эта команда использует docker compose для запуска и управления приложением, определенным в файле docker-compose.yaml. Она позволяет легко разворачивать и управлять сложными Docker-приложениями

18. `sudo docker compose up -d`

-d - Параметр -d в команде docker-compose up означает демонизирование процесса — запуск контейнеров в фоновом режиме.

![image](https://github.com/user-attachments/assets/02180457-23a3-4c8f-991f-21870df72174)
![image](https://github.com/user-attachments/assets/4fd6db97-83f1-44ab-8ac7-5037f8216ebc)

19. `sudo docker compose stop`

Команда останавливает запущенные контейнеры без их удаления.

![image](https://github.com/user-attachments/assets/1780a7b6-d2d3-430f-95e2-146f15475e63)

20. `sudo docker compose down`

Используемая команда для остановки и удаления контейнеров, сетей и томов, определенных в файле docker-compose.yml.

![image](https://github.com/user-attachments/assets/c6e4cb97-da32-4921-ab69-bebe32e95932)

21. `sudo docker compose ps`

Команда показывает информацию о контейнерах, управляемых Docker Compose, определенных в файле docker-compose.yml.

![image (3)](https://github.com/user-attachments/assets/e67a92a6-ab97-4298-b3e7-dead166fd241)

22. `pwd`

Команда выводит на экран абсолютный путь к текущей рабочей директории.

![image](https://github.com/user-attachments/assets/8fccf0ff-80b0-4306-b05d-30db6d36ac67)

23. `sudo git clone https://github.com/demidovas/demidova`

При помощи этой команды происходит комирование репрозитория с Github.

![image](https://github.com/user-attachments/assets/65b35082-eb1a-4d79-9acd-30f72877aa84)

Также была использована команда ls для просмотра файлов в папке.

23. `sudo vi docker-compose.yaml`

Команда предназначена для открытия или создания файла docker-compose.yaml в текстовом редакторе vi с правами суперпользователя (root).

![image](https://github.com/user-attachments/assets/9a5f1463-78d3-479d-acb6-ee22979642bb)
![image](https://github.com/user-attachments/assets/13759659-0868-4a56-9b8e-847602b94c51)

24. `sudo vi prometeus.yaml`

Команда также используется для открытия или создания файла с именем prometheus.yaml в текстовом редакторе vi с правами суперпользователя (root).

![image (7)](https://github.com/user-attachments/assets/e3f4daef-f803-4153-bdc2-8f767b72f036)
![image](https://github.com/user-attachments/assets/6fd77001-63cb-4e96-87f2-a4b1d1cf5f88)

25. `sudo vi prometeus.yaml`

Команда также используется для открытия или создания файла с именем prometheus.yaml в текстовом редакторе vi с правами суперпользователя (root).

![image (6)](https://github.com/user-attachments/assets/16eddc9b-28f4-45ab-b923-9df43bf62a6d)
![image](https://github.com/user-attachments/assets/6bce1916-d062-4ffc-8350-1f7e5595d0ba)

# Графана

Сайт: localhost:3000 Пользователь и пароль: admin

Зайдя на сайт, преобразует Dashboards для создания Dashboard.

![image](https://github.com/user-attachments/assets/aeb6845b-8a02-420d-bf72-5bd36cf9c5e9)

Следующий шаг: +Добавить визуализацию, после Настройте новый источник данных и вы преобразуете Prometheus.

![image](https://github.com/user-attachments/assets/69659950-8482-4b4d-92aa-0baa2625adb6)

Настройка: Соединение: `http://prometheus:9090` Аутентификация:`Basic authentication`

В заключение`Save & test`

![image](https://github.com/user-attachments/assets/cae0fa34-0730-4a82-ae83-7b5c20827cfd)

Далее, спомощью `Import dashboardсозданного Dashboard` импортируется.

`Find and import dashboards for common applications at grafana.com/dashboards: 1860`

![image](https://github.com/user-attachments/assets/b219fd4c-9129-4c91-81af-0894c39e3419)

В конце `Select Prometheusконцов Import.`

![image](https://github.com/user-attachments/assets/0c420bee-12c9-4b79-ac17-877bb8e56cd3)

# VictoriaMetrics

Точно также с добавлением `prometheus в grafana` была добавлена `victoriametrics`. В созданном Dashboard нет данных, что нормально.

![image](https://github.com/user-attachments/assets/2691459f-38ff-42f1-a594-3ec963e450bd)

26. `echo -e "# TYPE light_metric1 gauge\nlight_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus`

Эта команда отправляет метрику Prometheus в систему, работающую по адресу `http://localhost:8428`

![image (8)](https://github.com/user-attachments/assets/066cef41-1e89-445e-a1ea-a3f0ebc5addc)

Далее был осуществлен переход на `http://localhost:8428` - vmui

![image](https://github.com/user-attachments/assets/5fba58d1-1951-4407-8b70-e95d5e724876)

После, перейдя обратно в Grafana, были добавлены данные victoriametr

![image](https://github.com/user-attachments/assets/4825623d-ce5a-420a-a51b-f2444b427715)
