# Docker tips

## Remove unnamed images `<none>`

Можно использовать в cronjob для запуска раз в день для сохранения места на хосте

```bashag-0-1fo3ak3kvag-1-1fo3ak3kvag-0-1fo3ak3kvag-1-1fo3ak3kv
docker images --no-trunc | grep '<none>' | awk '{ print $3 }' | xargs -r docker rmi
```

## Add user to group of docker

Для работы с докером без sudo, требуется logout/login

```bash
sudo gpasswd -a $USER docker
```


## Delete old/unused containers, volumes and networks

Удалить все неиспользуемые containers, networks, images, volumes созданные до определённой даты

Например, те которые были созданы позднее чем 15 дней
```bash
docker system prune --filter="until=$(/usr/bin/date --date='15 days ago' -Iseconds)" --volumes --force
```
`until (<timestamp>)` - only remove containers, images, and networks created before given timestamp

Можно использовать в cronjob для запуска по расписанию
