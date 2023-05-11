# Стек Promtail + Loki + ClickHouse + Grafana
## Установка

1. Запускаем композ: `docker-compose up -d`
2. Устанавливаем Promtail:
        
    *  ``` curl -s https://api.github.com/repos/grafana/loki/releases/latest | grep browser_download_url |  cut -d '"' -f 4 | grep promtail-linux-amd64.zip | wget -i - ```
    * ``` unzip promtail-linux-amd64.zip && sudo mv promtail-linux-amd64 /usr/local/bin/promtail ```
    * ``` cp ./promtail/promtail-local-config.yaml /etc/``` для примера добавлены логи от nginx
    * сервис для Promtail ``` cp ./promtail/promtail.service /etc/systemd/system/ ```
    * ``` systemctl daemon-reload && systemctl start promtail.service ```

3. Подключение Loki к Grafana `config > data sources > loki > URL: <iphost>:3100` в Explore увидим результат `Log browser`
4. Так же через панель iphost:3100 подключим Loki: `data sources > Logs > URL <iphost>:3100`
5. Можно запустить вебморду для ClickHouse - Tabix: `docker exec -it clickhouse-server /bin/bash` > `nano /etc/clickhouse-server/config.xml` > Чтобы установить Tabix, достаточно в config.xml раскомментировать тег  <http_server_default_response...>, который будет подгружать Tabix. И перезапустить ClickHouse: `clickhouse restart` Теперь Tabix доступен по ссылке: `<iphost>:8123` user: qryn pass: demo 