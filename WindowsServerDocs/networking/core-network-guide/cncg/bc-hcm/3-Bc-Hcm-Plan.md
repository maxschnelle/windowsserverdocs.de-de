---
title: BranchCache-gehosteten Cachemodus Planung der Bereitstellung
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e645dd96ec85e3a23df6717cfa43d7627cb938e7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>BranchCache-gehosteten Cachemodus Planung der Bereitstellung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema können Sie die Planung der Bereitstellung von BranchCache im Modus für gehostete Caches.

>[!IMPORTANT]
>Der gehosteten Cacheserver muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.

Bevor Sie den gehosteten Cacheserver bereitstellen, müssen Sie Folgendes planen:

- [Planen der grundlegenden Serverkonfiguration](#bkmk_basic)

- [Planen der Domänenzugriff](#bkmk_domain)

- [Planen Sie die Position und Größe des gehosteten Caches](#bkmk_cachelocation)

- [Planen Sie die Freigabe, werden die Pakete Inhaltsserver kopiert werden](#bkmk_package)

- [Planen der prehashing und Daten Paket-auf-Inhaltsserver](#bkmk_prehash)

## <a name="bkmk_basic"></a>Planen der grundlegenden Serverkonfiguration
  
Wenn Sie, zur Verwendung von eines vorhandenen Servers in der Zweigstelle als den gehosteten Cacheserver beabsichtigen, müssen Sie keine dieser Schritt bei der Planung, ausgeführt werden, da der Computer bereits mit dem Namen und eine IP-Adresskonfiguration.

Nach der Installation von Windows Server 2016 auf Ihrer gehosteten Cacheserver müssen Sie Umbenennen des Computers und zuweisen und konfigurieren eine statische IP-Adresse für den lokalen Computer.

>[!NOTE]
>In diesem Handbuch wird der gehostete Cacheserver HCS1, mit dem Namen jedoch einen Servernamen verwendet werden soll, der für Ihre Bereitstellung geeignet ist.

## <a name="bkmk_domain"></a>Planen der Domänenzugriff

Wenn Sie, zur Verwendung von eines vorhandenen Servers in der Zweigstelle als den gehosteten Cacheserver beabsichtigen müssen nicht Sie diesen Schritt bei der Planung, ausführen, wenn der Computer derzeit nicht mit der Domäne angehört.
  
Um mit der Domäne anmelden zu können, muss der Computer einen Domänenmitgliedscomputer sein und muss das Benutzerkonto in AD DS vor der Anmeldung erstellt werden. Darüber hinaus müssen Sie die der Beitritt zur Domäne mit einem Konto, die Mitglied der entsprechenden Gruppe verfügt.

## <a name="bkmk_cachelocation"></a>Planen Sie die Position und Größe des gehosteten Caches

HCS1 ermitteln Sie, wo auf Ihrer gehosteten Cacheserver Suche nach dem gehosteten Cache. Entscheiden Sie z. B. die Festplatte, Volume und Speicherort des Ordners, in dem den Cache gespeichert werden sollen.

Darüber hinaus entscheiden Sie, wie viel Prozent des Speicherplatzes, die Sie für den gehosteten Cache zuweisen möchten.

## <a name="bkmk_package"></a>Planen Sie die Freigabe, werden die Pakete Inhaltsserver kopiert werden

Nach der Erstellung von Datenpaketen auf der Inhaltsserver müssen Sie sie über das Netzwerk auf eine Freigabe auf Ihrer gehosteten Cacheserver kopieren.

Planen Sie den Speicherort des Ordners und Freigabeberechtigungen für den freigegebenen Ordner. Darüber hinaus, wenn Ihre Inhalte Server, eine große Menge an Daten hosten und die Pakete, die Sie erstellen große Dateien werden, den Kopiervorgang Spitzenzeiten Off\ – ausführen möchten Sie, damit von den Kopiervorgang während einer WAN-Bandbreite nicht verwendet wird, wenn andere Personen die Bandbreite für normalen Betrieb verwenden müssen.

## <a name="bkmk_prehash"></a>Planen der prehashing und Daten Paket-auf-Inhaltsserver

Bevor Sie Inhalte auf der Inhaltsserver vorab der Hashfunktion unterziehen, müssen Sie ermitteln, die Ordner und Dateien, die Inhalte enthalten, die Sie dem Datenpaket hinzufügen möchten. 

Darüber hinaus müssen Sie auf den Speicherort des lokalen Ordners planen, in denen Datenpakete gespeichert werden können, bevor sie für den gehosteten Cacheserver kopiert werden.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md).
