---
title: Planung der Bereitstellung des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 476aa5f87436cd777ae6aa6fa2db70ace623deb7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956017"
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>Planung der Bereitstellung des BranchCache-Modus „Gehosteter Cache“

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können dieses Thema verwenden, um die Bereitstellung von BranchCache im Modus "gehosteter Cache" zu planen.

>[!IMPORTANT]
>Auf dem gehosteten Cache Server muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.

Bevor Sie den gehosteten Cache Server bereitstellen, müssen Sie die folgenden Elemente planen:

- [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)

- [Planen des Domänen Zugriffs](#bkmk_domain)

- [Planen Sie den Speicherort und die Größe des gehosteten Caches.](#bkmk_cachelocation)

- [Planen der Freigabe, in die die Inhalts Server Pakete kopiert werden sollen](#bkmk_package)

- [Planen von prähash-und Datenpaket Erstellung auf Inhalts Servern](#bkmk_prehash)

## <a name="plan-basic-server-configuration"></a><a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration

Wenn Sie beabsichtigen, einen vorhandenen Server in Ihrer Zweigstelle als gehosteten Cache Server zu verwenden, müssen Sie diesen Planungsschritt nicht ausführen, da der Computer bereits mit einer IP-Adress Konfiguration benannt ist und über eine IP-Adress Konfiguration verfügt.

Nachdem Sie Windows Server 2016 auf dem gehosteten Cache Server installiert haben, müssen Sie den Computer umbenennen und eine statische IP-Adresse für den lokalen Computer zuweisen und konfigurieren.

>[!NOTE]
>In diesem Handbuch heißt der gehostete Cache Server HCS1. Sie sollten jedoch einen Servernamen verwenden, der für Ihre Bereitstellung geeignet ist.

## <a name="plan-domain-access"></a><a name="bkmk_domain"></a>Planen des Domänen Zugriffs

Wenn Sie beabsichtigen, einen vorhandenen Server in Ihrer Zweigstelle als gehosteten Cache Server zu verwenden, müssen Sie diesen Planungsschritt nicht ausführen, es sei denn, der Computer ist derzeit nicht der Domäne beigetreten.

Damit sich der Computer bei der Domäne anmelden kann, muss er Mitglied der Domäne sein, und das Benutzerkonto muss vor der Anmeldung in AD DS erstellt worden sein. Außerdem müssen Sie den Computer mit einem Konto, das über die entsprechende Gruppenmitgliedschaft verfügt, der Domäne hinzufügen.

## <a name="plan-the-location-and-size-of-the-hosted-cache"></a><a name="bkmk_cachelocation"></a>Planen Sie den Speicherort und die Größe des gehosteten Caches.

Legen Sie auf HCS1 fest, wo der gehostete Cache Server den gehosteten Cache Server finden soll. Entscheiden Sie sich beispielsweise für die Festplatte, das Volume und den Speicherort des Ordners, in der der Cache gespeichert werden soll.

Außerdem müssen Sie entscheiden, welcher Prozentsatz des Speicherplatzes für den gehosteten Cache belegt werden soll.

## <a name="plan-the-share-to-which-the-content-server-packages-are-to-be-copied"></a><a name="bkmk_package"></a>Planen der Freigabe, in die die Inhalts Server Pakete kopiert werden sollen

Nachdem Sie Datenpakete auf Ihren Inhalts Servern erstellt haben, müssen Sie Sie über das Netzwerk in eine Freigabe auf dem gehosteten Cache Server kopieren.

Planen Sie den Speicherort des Ordners und die Freigabe Berechtigungen für den freigegebenen Ordner. Wenn Ihre Inhalts Server außerdem eine große Datenmenge hosten und die von Ihnen erstellten Pakete große Dateien sind, planen Sie die Ausführung des Kopiervorgangs außerhalb von \ – Spitzenzeiten, damit die WAN-Bandbreite nicht während des Kopiervorgangs von anderen Benutzern genutzt wird, wenn andere die Bandbreite für normale Geschäftsvorgänge benötigen.

## <a name="plan-prehashing-and-data-package-creation-on-content-servers"></a><a name="bkmk_prehash"></a>Planen von prähash-und Datenpaket Erstellung auf Inhalts Servern

Vor dem vorab Hash von Inhalten auf Ihren Inhalts Servern müssen Sie die Ordner und Dateien identifizieren, die Inhalte enthalten, die Sie dem Datenpaket hinzufügen möchten.

Außerdem müssen Sie den Speicherort des lokalen Ordners planen, in dem Sie die Datenpakete speichern können, bevor Sie Sie auf den gehosteten Cache Server kopieren.

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Bereitstellung des BranchCache-gehosteten Cache Modus](4-Bc-Hcm-Deployment.md).
