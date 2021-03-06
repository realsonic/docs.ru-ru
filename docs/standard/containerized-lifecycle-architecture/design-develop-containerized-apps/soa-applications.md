---
title: SOA приложений
description: Жизненный цикл контейнерного приложения Docker на основе платформы и средств Майкрософт
ms.prod: .net
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 5f60ff2fb1567d08b9e51e14ce5660a8e42f54aa
ms.sourcegitcommit: 2e8acae16ae802f2d6d04e3ce0a6dbf04e476513
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2018
---
# <a name="soa-applications"></a>SOA приложений

SOA был перегрузке термин и предназначен так много разных вещей для разных людей. Но по крайней мере и как общий знаменатель, SOA, или ориентации на службы, среднее структуры архитектуры приложения сегментируя несколько служб (чаще всего в качестве службы HTTP), которые могут быть классифицированы различных типов, такие как подсистемы или в других случаях, как и уровнями.

В настоящее время эти службы можно развернуть как контейнеры Docker, которая решает проблем, связанных с развертыванием, поскольку все зависимости, входят в образе контейнера. Тем не менее при необходимости масштабирования SOA, могут возникнуть трудности при развертывании на основе отдельные экземпляры. Это происходит, где Docker кластеризации программного обеспечения или orchestrator поможет вам. Мы рассмотрим это более подробно в следующем разделе после тщательного изучения микрослужбами подходов.

В конце дня кластерные решения контейнера удобны для обоих традиционной архитектуры SOA и для более сложных микрослужбами архитектуры, в которой каждый микрослужбу владеет его модели данных. И, благодаря несколько баз данных, вы также можно горизонтально масштабировать уровень данных вместо работы с базами данных монолитные, совместно используемые службами SOA. Тем не менее сведения о разделении данных — исключительно об архитектуре и разработке.


>[!div class="step-by-step"]
[Предыдущие] (state-and-data-in-docker-applications.md) [Далее] (координировать высокой масштабируемость availability.md)
