---
title: Übersicht über den BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 930a9b4872a7a79351055841a5d716dd99df0fa9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829511"
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>Übersicht über den BranchCache-Modus „Gehosteter Cache“

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können dieses Handbuch verwenden, einen gehosteten BranchCache-Cacheserver in einer Zweigstelle bereitstellen, in denen Computer einer Domäne beigetreten sind. Sie können in diesem Thema verwenden, um einen Überblick über den Bereitstellungsprozess BranchCache Hosted Cache Mode zu erhalten.

In dieser Übersicht umfasst die BranchCache-Infrastruktur, die Sie, sowie eine einfache schrittweise Überblick über die Bereitstellung benötigen.

## <a name="bkmk_components"></a>Gehostete Cacheserver Bereitstellungsinfrastruktur

In dieser Bereitstellung des gehosteten cacheservers bereitgestellt wird, in Active Directory Domain Services mithilfe von Dienstverbindungspunkten \(AD DS\), und Sie können mit BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, auf den freigegebenen Inhalt auf dem Web und unterziehen basierte Inhaltsserver, klicken Sie dann den Inhalt auf gehosteten Cacheservern vorab zu laden.

Die folgende Abbildung zeigt die Infrastruktur, die zum Bereitstellen eines gehosteten BranchCache-cacheservers erforderlich ist.

![Übersicht über die BranchCache Hosted Cache Mode](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> Obwohl diese Bereitstellung Inhaltsserver in einem Cloud-Rechenzentrum zeigt, können Sie dieses Handbuch verwenden, zum Bereitstellen eines gehosteten BranchCache-cacheservers, unabhängig davon, in der Inhaltsserver – in Ihrem Hauptbüro oder in einem Cloud-Verzeichnis bereitgestellt.

### <a name="hcs1-in-the-branch-office"></a>HCS1 in der Zweigstelle

Sie müssen diesen Computer als gehosteten Cacheserver konfigurieren. Wenn Sie entscheiden, Inhaltsserver Daten zu unterziehen, damit Sie den Inhalt auf die gehosteten Cacheserver vorab laden können, können Sie die Datenpakete importieren, die den Inhalt Ihrer Web- und Dateiservern enthalten.

### <a name="web1-in-the-cloud-data-center"></a>WEB1 im Cloud-Rechenzentrum

WEB1 ist eine BranchCache\-Inhaltsserver aktiviert. Wenn Sie entscheiden, Inhaltsserver Daten zu unterziehen, damit Sie den Inhalt auf die gehosteten Cacheserver vorab laden können, können Sie den freigegebenen Inhalt auf WEB1 unterziehen und dann ein Datenpaket, das Sie in HCS1 kopieren erstellen.

### <a name="file1-in-the-cloud-data-center"></a>"File1" im Cloud-Rechenzentrum

"File1" ist ein BranchCache\-Inhaltsserver aktiviert. Wenn Sie entscheiden, Inhaltsserver Daten zu unterziehen, damit Sie den Inhalt auf die gehosteten Cacheserver vorab laden können, können Sie unterziehen den freigegebenen Inhalt auf "file1" und dann ein Datenpaket, das Sie in HCS1 kopieren erstellen.
  
### <a name="dc1-in-the-main-office"></a>DC1 in der hauptniederlassung

DC1 ist ein Domänencontroller, und Sie müssen konfigurieren, die Standardrichtlinie der Domäne oder einer anderen Richtlinie, die für Ihre Bereitstellung mit BranchCache-gruppenrichtlinieneinstellungen zum automatische gehosteten Cache nach Dienstverbindungspunkt aktivieren besser geeignet ist.

Wenn Clientcomputer in der Verzweigung, auf die Gruppenrichtlinie aktualisiert verfügen, und mit dieser richtlinieneinstellung angewendet wird, suchen sie automatisch an und beginnen mit dem gehosteten Cacheserver in der Zweigstelle.

### <a name="client-computers-in-the-branch-office"></a>Client-Computer in der Zweigstelle

Sie müssen Gruppenrichtlinien aktualisieren, auf den Clientcomputern neue BranchCache-gruppenrichtlinieneinstellungen angewendet und können von Clients zum Suchen und verwenden den gehosteten Cacheserver.

## <a name="bkmk_overview"></a>Gehostete Cacheserver Übersicht über den Bereitstellungsprozess

>[!NOTE]
>Informationen zum Ausführen dieser Schritte finden Sie im Abschnitt [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md).

Der Prozess der Bereitstellung von BranchCache-gehosteter Cache Server erfolgt in dieser Phasen:

>[!NOTE]
>Einige der folgenden Schritte sind optional, wie z. B. die Schritte, die veranschaulichen, wie Sie Hashes und Vorabladen von Inhalt auf gehosteten Cacheservern. Wenn Sie BranchCache im Modus "gehosteter Cache" bereitstellen, müssen Sie nicht auf prehash Inhalte für Ihre Web- und Inhaltsserver, erstellen Sie ein Datenpaket und das Paket zu importieren, um die gehosteten Cacheserver mit Inhalt vorab laden. Die Schritte sind in diesem Abschnitt und im Abschnitt als optional gekennzeichnet [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md) , damit Sie sie nach Wunsch überspringen können.

1. Verwenden Sie Windows PowerShell-Befehle auf HCS1 um den Computer als gehosteten Cacheserver konfigurieren und Registrieren eines Dienstverbindungspunkts in Active Directory.

2. \(Optionale\) auf HCS1, wenn die BranchCache-Standardwerte der Bereitstellungsziele für den Server und dem gehosteten Cache, nicht übereinstimmen, konfigurieren die Menge an Speicherplatz, der für den gehosteten Cache zugeordnet werden soll. Konfigurieren Sie auch den Speicherort des Datenträgers, den Sie für den gehosteten Cache zu bevorzugen.

3. \(Optionale\) Hashes von Inhalten auf dem Inhaltsserver, Data-Pakete erstellen und Vorabladen von Inhalt auf dem gehosteten Cacheserver.

    > [!NOTE]
    > Prehashing und Vorabladen von Inhalt auf den gehosteten Cacheserver ist optional, jedoch bei Auswahl von zu unterziehen und vorab laden, werden, die unten beschriebenen Schritte ausgeführt müssen gelten für die Bereitstellung. \(Z. B. Wenn Sie nicht über Webserver verfügen, müssen nicht Sie die Schritte, die im Zusammenhang mit prehashing und Vorabladen von Inhalt von Webservern ausführen.\)

    1. Klicken Sie auf WEB1 unterziehen Sie Webserverinhalte, und erstellen Sie eines Datenpakets.

    2. Klicken Sie auf "file1" unterziehen Sie dateiserverinhalte, und erstellen Sie ein Datenpaket.

    3. Kopieren Sie die Datenpakete WEB1 "und" FILE1 "für den gehosteten Cacheserver HCS1.

    4. Importieren Sie auf HCS1 die Datenpakete aus, um den Datencache vorab zu laden.

4. Konfigurieren Sie auf DC1 mit domäneneinbindung Branch Office-Clientcomputern für den gehosteten Cachemodus durch Konfigurieren der Gruppenrichtlinie mit BranchCache-Richtlinieneinstellungen.

5. Aktualisieren Sie Gruppenrichtlinien auf den Clientcomputern.

Mit diesem Handbuch finden Sie [BranchCache Hosted Cache Mode Bereitstellungsplanung](3-Bc-Hcm-Plan.md).