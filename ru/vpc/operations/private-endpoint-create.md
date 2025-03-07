---
title: "Как создать сервисное подключение в {{ vpc-full-name }}"
description: "Следуя данной инструкции, вы сможете создать сервисное подключение (Private Endpoint) в VPC." 
---

# Создать сервисное подключение

{% include [vpc-pe-preview](../../_includes/vpc/pe-preview.md) %}


Для создания сервисного подключения необходима одна из следующих [ролей](../security/index.md#roles-list): 

* `vpc.admin`
* `vpc.privateAdmin`
* `admin`
* `vpc.privateEndpoints.editor`
* `vpc.privateEndpoints.admin`

Чтобы создать сервисное подключение:

{% list tabs group=instructions %}

- CLI {#cli}

  {% include [include](../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../_includes/default-catalogue.md) %}
  
  1. Посмотрите описание команды CLI для создания сервисного подключения:

      ```bash
      yc vpc private-endpoint create --help
      ```

  1. Создайте сервисное подключение к {{ objstorage-short-name }} в каталоге по умолчанию:

     ```bash
     yc vpc private-endpoint create \
        --name s3-vpc-link \
        --description "Private Endpoint to the Object Storage" \
        --network-name default-net \
        --object-storage 
     ```

     где:

     * `--network-name` — имя сети в которой будет создано сервисное подключение.
     * `--object-storage` — сервисное подключение к Object Storage. Другие типы сервисных подключей пока не доступны.

     При создании сервисного подключения можно использовать дополнительные параметры:

     * `--address-spec` — для указания IP-адреса и/или идентификатора подсети из которой будет взят IP-адрес для создаваемого сервисного подключения.
     * `--private-dns-records-enabled` — для указания нужно ли создавать отдельную DNS-запись для публичного FQDN сервиса. 


  1. Проверьте, что сервисное подключение создалось:

     ```bash
     yc vpc private-endpoint list
     ```
     
     Результат выполнения команды:

     ```text
     +----------------------+-------------+--------------------------------+
     |          ID          |    NAME     |          DESCRIPTION           |
     +----------------------+-------------+--------------------------------+
     | enpd7rq************* | s3-vpc-link | Private Endpoint to the Object |
     |                      |             | Storage                        |
     +----------------------+-------------+--------------------------------+
     ```

{% endlist %}
