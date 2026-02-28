## Тестовое задание MobilePark

Репозиторий разбит по директориям по смыслу трёх задач.

- `docker/` — задание по Dockerfile:
  - пример простого Flask‑приложения;
  - Dockerfile с правками и рекомендациями;
  - проверен локальной сборкой и запуском контейнера.
- `swarm/` — задание по Docker Swarm:
  - `docker-compose.swarm.yml` c описанием стека (Ubuntu‑клиент, PostgreSQL, Redis);
  - настройки ресурсов, логов, rolling‑update, placement по label `SERVERTYPE=worker`;
  - клиентский контейнер, из которого показано подключение к PostgreSQL и Redis.
- `ansible/` — задание по Ansible:
  - базовая подготовка трёх серверов (пользователи, SSH‑политики, пакеты);
  - установка фиксированной версии Docker из репозитория Ubuntu 22.04;
  - плейбук для инициализации Swarm и добавления worker‑нод.

### Как запускать локально (пример)

- **Dockerfile‑задание**:
  - перейти в каталог `docker/`;
  - собрать образ: `docker build -t mp-flask:test .`;
  - запустить контейнер: `docker run -d --rm -p 5000:5000 mp-flask:test`.

- **Swarm‑задание**:
  - на `mp-manager-01` должен быть инициализирован Docker Swarm и настроены label‑ы;
  - из каталога `swarm/` задеплоить стек:  
    `docker stack deploy -c docker-compose.swarm.yml mp-stack`.

- **Ansible‑задание**:
  - перейти в каталог `ansible/`;
  - проверить доступ: `ansible -m ping all`;
  - применить базовую конфигурацию: `ansible-playbook site.yml`;
  - при необходимости запустить плейбук Swarm: `ansible-playbook swarm.yml`.

