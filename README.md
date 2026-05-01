# Lighthouse Role

Роль Ansible для установки и настройки Lighthouse — веб-интерфейса для ClickHouse с использованием Nginx.

## Что делает роль

1. Устанавливает Nginx, Git и rsync
2. Клонирует репозиторий [Lighthouse](https://github.com/VKCOM/lighthouse)
3. Копирует статические файлы в директорию Nginx
4. Настраивает проксирование запросов к ClickHouse
5. Настраивает SELinux и права доступа
6. Запускает Nginx

## Требования

- Ansible 2.9+
- ClickHouse должен быть установлен и доступен по сети (порт 8123)
- Доступ к GitHub для клонирования репозитория

## Переменные

### defaults/main.yml

| Переменная | Значение по умолчанию | Описание |
|------------|------------------------|----------|
| `lighthouse_repo` | `https://github.com/VKCOM/lighthouse.git` | Репозиторий Lighthouse |
| `lighthouse_dir` | `/opt/lighthouse` | Директория установки Lighthouse |
| `nginx_html_dir` | `/usr/share/nginx/html` | Директория Nginx для статики |
| `clickhouse_host` | `127.0.0.1` | Адрес ClickHouse |

### Обязательные переменные (из playbook)

| Переменная | Описание |
|------------|----------|
| `clickhouse_host` | IP-адрес или хост ClickHouse |

## Использование

```yaml
- hosts: lighthouse
  become: true
  roles:
    - role: lighthouse-role
      vars:
        clickhouse_host: "IP-adress" # ваш IP адрес хоста
```

## Теги

```text
Тег	      | Описание
packages	| Установка зависимостей
download	| Клонирование репозитория Lighthouse
config	  | Настройка Nginx
selinux	  | Настройка SELinux
service	  | Запуск Nginx
```

## Проверка работы

После установки откройте в браузере:
```text
http://<IP_адрес_хоста>
```

## Установка

```bash
ansible-galaxy install git+https://github.com/IthnHuitn/lighthouse-role.git
```

## Автор 

## `IthnHuitn`