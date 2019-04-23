---
title: Planung der Bereitstellung des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e7232f8732e7476b955115741b5582a585dc6068
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890681"
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>Planung der Bereitstellung des BranchCache-Modus „Gehosteter Cache“

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können in diesem Thema verwenden, zum Planen der Bereitstellung von BranchCache im Modus für gehostete Caches.

>[!IMPORTANT]
>Der gehosteten Cacheserver muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.

Bevor Sie den gehosteten Cacheserver bereitstellen, müssen Sie Folgendes planen:

- [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)

- [Zugriff auf den Plan-Domäne](#bkmk_domain)

- [Planen Sie die Position und Größe des gehosteten Caches](#bkmk_cachelocation)

- [Planen Sie die Freigabe, die die Inhaltsserver-Pakete, die zu kopierenden sind](#bkmk_package)

- [Plan prehashing und Daten der paketerstellung auf Inhaltsserver](#bkmk_prehash)

## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration
  
Wenn Sie, zur Verwendung von eines vorhandenen Servers in der Zweigstelle als den gehosteten Cacheserver beabsichtigen, müssen Sie nicht diesen Schritt bei der Planung, ausgeführt werden, da der Computer ist bereits mit dem Namen und eine IP-Adresskonfiguration.

Nachdem Sie Windows Server 2016 auf den gehosteten Cacheserver installieren, müssen Sie Umbenennen des Computers und zuweisen und konfigurieren eine statische IP-Adresse für den lokalen Computer.

>[!NOTE]
>In diesem Handbuch wird der gehostete Cacheserver HCS1, mit dem Namen, aber Sie sollten einen Servernamen verwenden, der für Ihre Bereitstellung geeignet ist.

## <a name="bkmk_domain"></a>Zugriff auf den Plan-Domäne

Wenn Sie, zur Verwendung von eines vorhandenen Servers in der Zweigstelle als den gehosteten Cacheserver beabsichtigen müssen nicht Sie führen Sie diesen Schritt bei der Planung, es sei denn, der Computer derzeit nicht mit der Domäne verknüpft ist.
  
Zum Anmelden an der Domäne der Computer muss ein Domänenmitgliedscomputer sein, und das Benutzerkonto muss vor der Anmeldung in AD DS erstellt werden. Darüber hinaus müssen Sie die der Beitritt zur Domäne mit einem Konto an, die die entsprechende Gruppe Mitglied ist.

## <a name="bkmk_cachelocation"></a>Planen Sie die Position und Größe des gehosteten Caches

HCS1 ermitteln Sie, in dem auf den gehosteten Cacheserver sollen den gehosteten Cache zu suchen. Entscheiden Sie beispielsweise die Festplatte, Datenträger und Speicherort des Ordners, in dem den Cache gespeichert werden sollen.

Darüber hinaus entscheiden Sie, welcher Prozentsatz des Speicherplatzes, die Sie für den gehosteten Cache zuordnen möchten.

## <a name="bkmk_package"></a>Planen Sie die Freigabe, die die Inhaltsserver-Pakete, die zu kopierenden sind

Nachdem Sie auf der Inhaltsserver Datenpakete erstellt haben, müssen Sie diese über das Netzwerk auf eine Freigabe für den gehosteten Cacheserver kopieren.

Planen Sie den Ordner und Freigabeberechtigungen für den freigegebenen Ordner. Darüber hinaus, wenn der Inhaltsserver eine große Menge von Daten hosten und die Pakete, die Sie erstellen großer Dateien werden, den Kopiervorgang während der Off\ – Spitzenzeiten ausführen möchten Sie, damit Sie WAN-Bandbreite nicht von den Kopiervorgang während eines Zeitraums verarbeitet wird, wenn andere Personen verwenden müssen  die Bandbreite für den normalen Geschäftsbetrieb.

## <a name="bkmk_prehash"></a>Plan prehashing und Daten der paketerstellung auf Inhaltsserver

Bevor Sie Inhalte auf der Inhaltsserver unterziehen, müssen Sie ermitteln, die Ordner und Dateien, die Inhalt enthalten, die Sie das Paket hinzufügen möchten. 

Darüber hinaus müssen Sie auf den lokalen Ordner an planen, in dem Sie die Datenpakete speichern können, bevor sie für den gehosteten Cacheserver kopiert werden.

Mit diesem Handbuch finden Sie [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md).
