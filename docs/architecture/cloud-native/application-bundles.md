---
title: Пакеты приложений, ориентированных на облако
description: Создание архитектуры облачных приложений .NET для Azure | Пакеты облачных приложений машинного кода
ms.date: 01/19/2021
ms.openlocfilehash: d3427ddf82b65dd274ef253749a9b87864092a0a
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506140"
---
# <a name="cloud-native-application-bundles"></a>Пакеты приложений, ориентированных на облако

Ключевым свойством облачных приложений является то, что они используют возможности облака для ускорения разработки. Такая схема часто означает, что в полном приложении используются различные виды технологий. Приложения могут поставляться в контейнерах DOCKER. Некоторые службы могут использовать функции Azure, тогда как другие могут работать непосредственно с виртуальными машинами, выделенными на больших серверах с аппаратным ускорением GPU. Ни одно из двух собственных приложений в облаке не одинаково, поэтому было сложно предоставить единый механизм для их отправки.

Контейнеры DOCKER могут выполняться в Kubernetes с помощью диаграммы Helm для развертывания. Функции Azure можно выделить с помощью шаблонов terraform. Наконец, виртуальные машины могут быть выделены с помощью terraform, но созданы с помощью Ansible. Это большое разнообразие технологий, и нет возможности упаковать их вместе в разумный пакет. До настоящего момента.

Облачные пакеты приложений (КНАБС) являются совместными усилиями многих компаний, таких как Microsoft, Docker и HashiCorp, для разработки спецификации для упаковки распределенных приложений.

Усилия были объявлены в декабре 2018, поэтому по-прежнему остается довольно много усилий, чтобы сделать работу с большим сообществом. Однако уже есть [Открытая спецификация](https://github.com/deislabs/cnab-spec) и эталонная реализация, известная как [сумку](https://duffle.sh/). Это средство, написанное на Go, является совместным усилиями между DOCKER и Майкрософт.

КНАБС может содержать различные технологии установки. Этот аспект позволяет Helm диаграммам, шаблонам terraform и Ansible модули PlayBook сосуществовать в одном пакете. После сборки пакеты являются автономными и переносимыми. их можно установить с USB-носителя.  Пакеты криптографически подписываются, чтобы убедиться, что они берутся из утвержденной им стороны.

Ядром КНАБ является файл с именем `bundle.json` . Этот файл определяет содержимое пакета, terraform или изображения или что-либо другое. На рис. 11-9 определен КНАБ, вызывающий некоторые terraform. Однако обратите внимание, что он фактически определяет изображение вызова, которое используется для вызова terraform. При создании пакета файл DOCKER, расположенный в каталоге *КНАБ* , встроен в образ DOCKER, который будет включен в пакет. Установка terraform в контейнер DOCKER в пакете означает, что пользователям не нужно устанавливать terraform на компьютере для запуска объединения.

```json
{
    "name": "terraform",
    "version": "0.1.0",
    "schemaVersion": "v1.0.0-WD",
    "parameters": {
        "backend": {
            "type": "boolean",
            "defaultValue": false,
            "destination": {
                "env": "TF_VAR_backend"
            }
        }
    },
    "invocationImages": [
        {
        "imageType": "docker",
        "image": "cnab/terraform:latest"
        }
    ],
    "credentials": {
        "tenant_id": {
            "env": "TF_VAR_tenant_id"
        },
        "client_id": {
            "env": "TF_VAR_client_id"
        },
        "client_secret": {
            "env": "TF_VAR_client_secret"
        },
        "subscription_id": {
            "env": "TF_VAR_subscription_id"
        },
        "ssh_authorized_key": {
            "env": "TF_VAR_ssh_authorized_key"
        }
    },
    "actions": {
        "status": {
            "modifies": true
        }
    }
}
```

**Рис. 10-18** . пример файла terraform

`bundle.json`Также определяет набор параметров, которые передаются в terraform. Параметризация пакета позволяет устанавливать в разных средах.

Формат КНАБ также является гибким, что позволяет использовать его в любом облаке. Его можно использовать и в локальных решениях, таких как [OpenStack](https://www.openstack.org/).

## <a name="devops-decisions"></a>DevOps решения

В DevOps пространстве есть много замечательных средств, а также еще более потрясающие книги и документы о том, как их можно достичь. Чтобы приступить к работе в DevOps, можно перейти к [проекту Phoenix](https://www.oreilly.com/library/view/the-phoenix-project/9781457191350/), который следует за преобразованием вымышленной компании из Нупс в DevOps. Одна из них: DevOps больше не является «полезной» при развертывании сложных облачных приложений в машинном код. Это требование, и его следует планировать и перенаследовать в начале любого проекта.

## <a name="references"></a>Ссылки

- [Azure DevOps](https://azure.microsoft.com/services/devops/)
- [Azure Resource Manager](/azure/azure-resource-manager/management/overview)
- [Terraform](https://www.terraform.io/)
- [Azure CLI](/cli/azure/)

>[!div class="step-by-step"]
>[Назад](infrastructure-as-code.md)
>[Вперед](summary.md)
