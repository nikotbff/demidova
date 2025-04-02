# demidova

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

`cd grafana_stack_for_docker`
Эта команда использует утилиту mkdir для создания каталогов "директорий" на файловой системе.

`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`
Эта команда использует утилиту mkdir с опцией -p и расширением фигурных скобок "brace expansion" для создания нескольких каталогов в файловой системе.

`sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`
Эта команда использует утилиту chown для изменения владельца "owner" и группы "group" файлов и каталогов.

`sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`
Эта команда использует утилиту touch для создания пустого файла.

`touch /mnt/common_volume/grafana/grafana-config/grafana.ini`
Эта команда использует утилиту cp "copy" для копирования файлов.

`cp config/* /mnt/common_volume/swarm/grafana/config/`
Эта команда использует утилиту mv "move" для переименования файла, обычно приводя имя файла к стандартному или ожидаемому.

`mv grafana.yaml docker-compose.yaml`
Эта команда использует docker compose для запуска и управления приложением, определенным в файле docker-compose.yaml. Она позволяет легко разворачивать и управлять сложными Docker-приложениями

`sudo docker compose up -d`
-d - Параметр -d в команде docker-compose up означает демонизирование процесса — запуск контейнеров в фоновом режиме.

