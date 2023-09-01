## О проекте

Проект представляет собой docker-compose файл для запуска системы из minio s3 и nginx-s3-gateway.

## Требования
Необходимо иметь root-права, установленный docker-compose и curl.

## Использование
1. Создаём папку, которая позже будет примонтирована к контейнеру minio:
```mkdir -p ~/minio/data```
2. Затем, необходимо загрузить файл compose.yml при помощи curl:
```curl https://raw.githubusercontent.com/inq1337/minio-nginx/main/compose.yml > compose.yml
```
3. В этом файле, при помощи текстового редактора (например, nano), нужно отредактировать следующие строки, заменив значения на свои:
    ```services:
      s3:
        ...
        environment:
          - MINIO_ROOT_USER=LOGIN
          - MINIO_ROOT_PASSWORD=PASSWORD
          ...

      nginx-s3-gateway:
          ...
          environment:
          - S3_BUCKET_NAME=name
          - AWS_ACCESS_KEY_ID=LOGIN
          - AWS_SECRET_ACCESS_KEY=PASSWORD
          ...
    ```
4. Поссле этого, можно запускать docker-compose:
    ```docker compose up```

Панель управления minio будет доступна по адресу `http://адрес_машины:9090`
Сервис кеширования nginx будет доступен по адресу `http://адрес_машины:80`

5. После создания bucket'а с именем, соответствующим значению, подставленному в `S3_BUCKET_NAME=name` и загрузки в него файлов, они будут доступны из nginx
