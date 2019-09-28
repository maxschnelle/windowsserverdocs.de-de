---
title: Planung der Bereitstellung des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0fe55bc9971606559af652d592a91db7a89544a7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356371"
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

## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration
  
Wenn Sie beabsichtigen, einen vorhandenen Server in Ihrer Zweigstelle als gehosteten Cache Server zu verwenden, müssen Sie diesen Planungsschritt nicht ausführen, da der Computer bereits mit einer IP-Adress Konfiguration benannt ist und über eine IP-Adress Konfiguration verfügt.

Nachdem Sie Windows Server 2016 auf dem gehosteten Cache Server installiert haben, müssen Sie den Computer umbenennen und eine statische IP-Adresse für den lokalen Computer zuweisen und konfigurieren.

>[!NOTE]
>In diesem Handbuch heißt der gehostete Cache Server HCS1. Sie sollten jedoch einen Servernamen verwenden, der für Ihre Bereitstellung geeignet ist.

## <a name="bkmk_domain"></a>Planen des Domänen Zugriffs

Wenn Sie beabsichtigen, einen vorhandenen Server in Ihrer Zweigstelle als gehosteten Cache Server zu verwenden, müssen Sie diesen Planungsschritt nicht ausführen, es sei denn, der Computer ist derzeit nicht der Domäne beigetreten.
  
Wenn Sie sich bei der Domäne anmelden möchten, muss es sich bei dem Computer um einen Domänen Mitglieds Computer handeln, und das Benutzerkonto muss vor dem Anmeldeversuch in AD DS erstellt werden. Außerdem müssen Sie den Computer mit einem Konto, das über die entsprechende Gruppenmitgliedschaft verfügt, der Domäne hinzufügen.

## <a name="bkmk_cachelocation"></a>Planen Sie den Speicherort und die Größe des gehosteten Caches.

Legen Sie auf HCS1 fest, wo der gehostete Cache Server den gehosteten Cache Server finden soll. Entscheiden Sie sich beispielsweise für die Festplatte, das Volume und den Speicherort des Ordners, in der der Cache gespeichert werden soll.

Außerdem müssen Sie entscheiden, welcher Prozentsatz des Speicherplatzes für den gehosteten Cache belegt werden soll.

## <a name="bkmk_package"></a>Planen der Freigabe, in die die Inhalts Server Pakete kopiert werden sollen

Nachdem Sie Datenpakete auf Ihren Inhalts Servern erstellt haben, müssen Sie Sie über das Netzwerk in eine Freigabe auf dem gehosteten Cache Server kopieren.

Planen Sie den Speicherort des Ordners und die Freigabe Berechtigungen für den freigegebenen Ordner. Wenn Ihre Inhalts Server außerdem eine große Datenmenge hosten und die von Ihnen erstellten Pakete große Dateien sind, planen Sie die Ausführung des Kopiervorgangs außerhalb von \ –-Spitzenzeiten, damit die WAN-Bandbreite während einer Zeitspanne, in der andere Benutzer verwenden müssen, nicht durch den Kopiervorgang verbraucht wird.  die Bandbreite für den normalen Geschäftsbetrieb.

## <a name="bkmk_prehash"></a>Planen von prähash-und Datenpaket Erstellung auf Inhalts Servern

Vor dem vorab Hash von Inhalten auf Ihren Inhalts Servern müssen Sie die Ordner und Dateien identifizieren, die Inhalte enthalten, die Sie dem Datenpaket hinzufügen möchten. 

Außerdem müssen Sie den Speicherort des lokalen Ordners planen, in dem Sie die Datenpakete speichern können, bevor Sie Sie auf den gehosteten Cache Server kopieren.

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Bereitstellung des BranchCache-gehosteten Cache Modus](4-Bc-Hcm-Deployment.md).
