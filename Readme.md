# Hexlet Load Balancing Demo

## Пререквизиты

- Установленный Ansible
- Установленный [Vagrant](https://www.vagrantup.com/)

## Документация

- <https://docs.docker.com/engine/swarm/>
- [HAProxy](https://cbonte.github.io/haproxy-dconv/2.2/configuration.html>)
- [Traefik](https://doc.traefik.io/traefik/)

## Как запустить

Ставим роли и коллекции из Ansible Galaxy

```bash
cd ansible
ansible-galaxy install -r roles/requirements.yml
```

Запускаем виртуалки:

```bash
vagrant init
vagrant up
```

Собираем себе кластер Docker Swarm и играемся

При необходимости сбросить состояние виртуалки - перезапускаем Vagrant

```bash
vagrant destroy -f && vagrant up
```

## Как использовать

Предполагается, что у нас будет 3 ноды с Docker Swarm:

- 192.168.56.21 (node1)
- 192.168.56.22 (node2)
- 192.168.56.23 (node3)

И одна нода с установленным HAProxy под Load Balancer, с IP 192.168.56.50 (lb)

Конфиги, используемые в демо:

- `app/docker-compose.yml` - базовый stack-файл безо всяких наворотов;
- `app/docker-compose_traefik.yml` - stack-файл со сконфигурированным Traefik;
- `app/haproxy/haproxy-l4.cfg` - конфиг для HAProxy в режиме L4 балансировщика;
- `app/haproxy/haproxy-l7.cfg` - конфиг для HAProxy в режиме L7 балансировщика;

Конфиг HAProxy лежит в `/etc/haproxy/haproxy.cfg`

Запустить/перезапустить HAProxy можно командами `systemctl start haproxy` и `systemctl restart haproxy`, посмотреть логи - `journalctl -u haproxy`