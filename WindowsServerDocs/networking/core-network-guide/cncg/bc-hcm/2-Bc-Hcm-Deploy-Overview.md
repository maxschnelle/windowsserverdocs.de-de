---
title: BranchCache-gehosteten Cache Bereitstellung – Übersicht
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: feab3156b89637f64d1af0250df459533b1662c7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>BranchCache-gehosteten Cache Bereitstellung – Übersicht

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Handbuch können einen BranchCache-gehosteten Cacheserver in einer Zweigstelle bereitstellen, in denen Computer einer Domäne beigetreten sind. In diesem Thema können Sie um eine Übersicht über den Bereitstellungsprozess BranchCache Hosted Cache Mode zu erhalten.

In dieser Übersicht umfasst die BranchCache-Infrastruktur, die Sie, sowie eine einfache schrittweise Überblick über die Bereitstellung benötigen.

## <a name="bkmk_components"></a>Gehostete Cacheserver Bereitstellungsinfrastruktur

In dieser Bereitstellung Dienstverbindungspunkte in Active Directory Domain Services \(AD DS\), mit der gehosteten Cacheserver bereitgestellt wird und Sie haben die Möglichkeit mit BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, um den freigegebenen Inhalt auf Web- und Hashes basierte Inhaltsserver, und klicken Sie dann den Inhalt auf gehosteten Cacheserver laden.

Die folgende Abbildung zeigt die Infrastruktur, die zum Bereitstellen von BranchCache-gehosteten Cacheserver erforderlich ist.

![BranchCache Hosted Cache Mode (Übersicht)](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> Obwohl diese Bereitstellung Inhaltsserver in einem Cloud-Rechenzentrum zeigt, können Sie dieses Handbuch, zum Bereitstellen von BranchCache-gehosteten Cacheserver unabhängig davon, wo Sie Ihre Inhaltsserver – in Ihrem Hauptbüro oder in einem Cloud-Verzeichnis bereitstellen.

### <a name="hcs1-in-the-branch-office"></a>HCS1 in der Filiale

Sie müssen diesen Computer als gehosteten Cacheserver konfigurieren. Wenn Sie Inhaltsserver Daten vorab der Hashfunktion unterziehen, damit den Inhalt auf Ihrer gehosteten Cacheserver vorab laden möchten, können Sie Datenpakete importieren, die den Inhalt aus Ihrer Web- und Dateiservern enthalten.

### <a name="web1-in-the-cloud-data-center"></a>In der Cloud-Rechenzentrum WEB1

WEB1 ist BranchCache\-fähigen Inhaltsserver. Wenn Sie Inhaltsserver Daten vorab der Hashfunktion unterziehen, damit den Inhalt auf Ihrer gehosteten Cacheserver vorab laden möchten, können Sie den freigegebenen Inhalt auf WEB1 Hashes und anschließend erstellen ein Pakets mit Daten, das in HCS1 kopiert.

### <a name="file1-in-the-cloud-data-center"></a>"File1" in der Cloud-Rechenzentrum

"File1" ist ein BranchCache\-fähiger Inhaltsserver. Wenn Sie Inhaltsserver Daten vorab der Hashfunktion unterziehen, damit den Inhalt auf Ihrer gehosteten Cacheserver vorab laden möchten, können Sie vorab der Hashfunktion unterziehen des freigegebenen Inhalts auf "file1" und dann erstellen ein Pakets mit Daten, das in HCS1 kopiert.
  
### <a name="dc1-in-the-main-office"></a>DC1 in der zentrale

DC1 ist ein Domänencontroller, und konfigurieren Sie die Standarddomänenrichtlinie oder einer anderen Richtlinie, die besser geeignet für die Bereitstellung mit BranchCache-gruppenrichtlinieneinstellungen automatische gehosteten Cache nach Dienstverbindungspunkt aktiviert ist.

Wenn Clientcomputer in der Zweigstelle Gruppenrichtlinien aktualisiert haben und diese Einstellung angewendet wird, suchen sie automatisch an und beginnen mit dem gehosteten Cacheserver in der Filiale.

### <a name="client-computers-in-the-branch-office"></a>Clientcomputer in der Filiale

Sie müssen Gruppenrichtlinien auf Clientcomputern neue BranchCache-gruppenrichtlinieneinstellungen angewendet und ermöglichen Clients suchen und verwenden den gehosteten Cacheserver aktualisieren.

## <a name="bkmk_overview"></a>Gehostete Cacheserver Prozess Bereitstellungsübersicht

>[!NOTE]
>Die Details zum Ausführen dieser Schritte finden Sie in den Abschnitt [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md).

Der Prozess der Bereitstellung einer BranchCache-gehosteten Cacheserver erfolgt in diesen Phasen:

>[!NOTE]
>Einige der folgenden Schritte sind optional, z. B. die Schritte, die veranschaulichen, wie Sie prehashing und Vorabladen von Inhalt auf gehosteten Cacheserver. Wenn Sie BranchCache im Modus für gehostete Caches bereitstellen, sind Sie nicht erforderlich, um prehash Inhalt auf Ihren Web- und Inhalten Servern zum Erstellen eines Datenpakets und das Paket mit Daten zu importieren, um die gehosteten Cacheserver mit Inhalt vorab laden. Die Schritte sind als optionale aufgeführt, in diesem Abschnitt und im Abschnitt [BranchCache Hosted Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md) , damit Sie können Sie auf Wunsch überspringen.

1. Verwenden Sie auf HCS1 Windows PowerShell-Befehle, um den Computer als gehosteten Cacheserver konfigurieren und Registrieren eines Dienstverbindungspunkts in Active Directory.

2. \(Optional\) auf HCS1, wenn die BranchCache-Standardwerte der Bereitstellungsziele für den Server und dem gehosteten Cache, nicht übereinstimmen, konfigurieren die Menge an Speicherplatz, der für den gehosteten Cache zugeordnet werden soll. Auch konfigurieren Sie, die den Speicherort, die Sie für den gehosteten Cache bevorzugen.

3. \(Optional\) Prehash Inhalte auf Inhaltsserver, Erstellen von Datenpaketen und vorab geladene Inhalt auf dem gehosteten Cacheserver.

    > [!NOTE]
    > Prehashing und Vorabladen von Inhalt auf Ihrer gehosteten Cacheserver ist optional, jedoch wenn Sie vorab der Hashfunktion unterziehen und vorab geladene, Sie werden die Schritte, die ausgeführt müssen für Ihre Bereitstellung anwendbar sind. \ (Wenn beispielsweise Sie nicht über Webserver verfügen, Sie brauchen die Schritte im Zusammenhang mit prehashing und Vorabladen von Inhalt Webserver ausführen. \)

    1. Auf WEB1 Hashes Webserver-Inhalt, und erstellen Sie ein Datenpaket.

    2. Auf FILE1 dateiserverinhalte prehashing und ein Datenpaket erstellen.

    3. Kopieren Sie von WEB1 und "file1" die Datenpakete für den gehosteten Cacheserver HCS1.

    4. Importieren Sie auf HCS1 die Datenpakete, um den Datencache vorab laden.

4. Konfigurieren Sie auf DC1 Domäne Branch Office-Clientcomputern für den Modus für gehostete Caches durch Konfigurieren der Gruppenrichtlinie mit BranchCache-Richtlinien.

5. Aktualisieren Sie Gruppenrichtlinien auf den Clientcomputern.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [BranchCache Hosted Cache Mode Planen der Bereitstellung](3-Bc-Hcm-Plan.md).