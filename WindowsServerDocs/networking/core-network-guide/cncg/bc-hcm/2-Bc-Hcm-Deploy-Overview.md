---
title: Übersicht über den BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dc6ade92eb5fe04271033973911ccb98e871d236
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406375"
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>Übersicht über den BranchCache-Modus „Gehosteter Cache“

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit dieser Anleitung können Sie einen gehosteten BranchCache-Cache Server in einer Zweigstelle bereitstellen, in der Computer einer Domäne hinzugefügt werden. In diesem Thema erhalten Sie einen Überblick über den BranchCache-Bereitstellungs Prozess für gehostete Caches.

Diese Übersicht enthält die BranchCache-Infrastruktur, die Sie benötigen, sowie eine einfache Schritt-für-Schritt-Übersicht über die Bereitstellung.

## <a name="bkmk_components"></a>Gehostete Cache Server-Bereitstellungs Infrastruktur

In dieser Bereitstellung wird der gehostete Cache Server mithilfe von Dienst Verbindungs Punkten in Active Directory Domain Services \(AD DS\)bereitgestellt, und Sie haben die Möglichkeit, mit BranchCache in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 einen prähash für den freigegebenen Inhalt auf Web-und dateibasierten Inhalts Servern durchzusetzen und den Inhalt auf gehosteten Cache Servern vorab zu laden.

Die folgende Abbildung zeigt die Infrastruktur, die zum Bereitstellen eines gehosteten BranchCache-Cache Servers erforderlich ist.

![BranchCache: Übersicht über den gehosteten Cache Modus](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> Obwohl bei dieser Bereitstellung Inhalts Server in einem cloudrechenzentrum angezeigt werden, können Sie diese Anleitung zum Bereitstellen eines gehosteten BranchCache-Cache Servers verwenden, unabhängig davon, wo Sie Ihre Inhalts Server bereitstellen – in ihrer Zentrale oder an einem cloudspeicherort.

### <a name="hcs1-in-the-branch-office"></a>HCS1 in der Zweigstelle

Sie müssen diesen Computer als gehosteten Cache Server konfigurieren. Wenn Sie sich für das vorab Hash der Inhalts Serverdaten entscheiden, sodass Sie den Inhalt auf den gehosteten Cache Servern vorab laden können, können Sie Datenpakete importieren, die den Inhalt von den Web-und Dateiservern enthalten.

### <a name="web1-in-the-cloud-data-center"></a>WEB1 im cloudrechenzentrum

WEB1 ist ein\-aktivierter BranchCache-Inhalts Server. Wenn Sie sich für das vorab Hash der Inhalts Serverdaten entscheiden, sodass Sie den Inhalt auf den gehosteten Cache Servern vorab laden können, können Sie den freigegebenen Inhalt auf WEB1 vorab mit einem Hash versehen und dann ein Datenpaket erstellen, das Sie in HCS1 kopieren.

### <a name="file1-in-the-cloud-data-center"></a>File1 im cloudrechenzentrum

File1 ist ein\-aktivierter BranchCache-Inhalts Server. Wenn Sie sich für das vorab Hash der Inhalts Serverdaten entscheiden, sodass Sie den Inhalt auf den gehosteten Cache Servern vorab laden können, können Sie den freigegebenen Inhalt auf file1 vorab mit einem Hash versehen und dann ein Datenpaket erstellen, das Sie in HCS1 kopieren.
  
### <a name="dc1-in-the-main-office"></a>DC1 in der zentrale

DC1 ist ein Domänen Controller, und Sie müssen die Standard Domänen Richtlinie oder eine andere Richtlinie konfigurieren, die für die Bereitstellung geeigneter ist, mit BranchCache-Gruppenrichtlinie Einstellungen, um die automatische Ermittlung von gehosteten Caches durch den Dienst Verbindungspunkt zu aktivieren.

Wenn die Client Computer in der Verzweigung Gruppenrichtlinie aktualisiert haben und diese Richtlinien Einstellung angewendet wird, finden Sie automatisch den gehosteten Cache Server in der Zweigstelle und verwenden diesen.

### <a name="client-computers-in-the-branch-office"></a>Client Computer in der Zweigstelle

Sie müssen Gruppenrichtlinie auf Client Computern aktualisieren, um neue BranchCache-Gruppenrichtlinie Einstellungen anzuwenden und Clients das Auffinden und Verwenden des gehosteten Cache Servers zu ermöglichen.

## <a name="bkmk_overview"></a>Übersicht über den Bereitstellung des gehosteten Cache Servers

>[!NOTE]
>Ausführliche Informationen zum Ausführen dieser Schritte finden Sie im Abschnitt Bereitstellung des [BranchCache-gehosteten Cache Modus](4-Bc-Hcm-Deployment.md).

Der Prozess der Bereitstellung eines gehosteten BranchCache-Cache Servers erfolgt in den folgenden Phasen:

>[!NOTE]
>Einige der unten aufgeführten Schritte sind optional, wie z. b. die Schritte, die veranschaulichen, wie Inhalt auf gehosteten Cache Servern vorab und vorab geladen wird. Wenn Sie BranchCache im Modus "gehosteter Cache" bereitstellen, ist es nicht erforderlich, Inhalte auf Ihren Web-und Datei Inhalts Servern vorzuführen, ein Datenpaket zu erstellen und das Datenpaket zu importieren, um die gehosteten Cache Server mit Inhalt vorab zu laden. Die Schritte werden in diesem Abschnitt und im Abschnitt [Bereitstellung des BranchCache-gehosteten Cache Modus](4-Bc-Hcm-Deployment.md) als optional angegeben, sodass Sie Sie bei Bedarf überspringen können.

1. Verwenden Sie auf HCS1 Windows PowerShell-Befehle, um den Computer als gehosteten Cache Server zu konfigurieren und einen Dienst Verbindungspunkt in Active Directory zu registrieren.

2. \(optionale\) auf HCS1, wenn die BranchCache-Standardwerte nicht mit ihren Bereitstellungs Zielen für den Server und den gehosteten Cache identisch sind, konfigurieren Sie die Menge des Speicherplatzes, den Sie für den gehosteten Cache zuordnen möchten. Konfigurieren Sie auch den Speicherort des Datenträgers, den Sie für den gehosteten Cache bevorzugen.

3. \(optional\) prähashinhalt von Inhalts Servern, Erstellen von Datenpaketen und vorab Laden von Inhalt auf dem gehosteten Cache Server.

    > [!NOTE]
    > Das vorab Hashing und vorab Laden von Inhalt auf dem gehosteten Cache Server ist optional. Wenn Sie sich jedoch für den Hashes und den vorab Ladevorgang entscheiden, müssen Sie alle nachfolgenden Schritte ausführen, die für Ihre Bereitstellung gelten. Wenn Sie z. b. nicht über Webserver verfügen, müssen Sie keine der Schritte im Zusammenhang mit dem vorab hashten und vorab Laden von Webserver Inhalten ausführen. \(\)

    1. Führen Sie auf WEB1 einen Hashes für Webserver Inhalt aus, und erstellen Sie ein Datenpaket.

    2. Führen Sie auf file1 einen prähash für Dateiserver Inhalt aus, und erstellen Sie ein Datenpaket.

    3. Kopieren Sie die Datenpakete von WEB1 und file1 auf den gehosteten Cache Server HCS1.

    4. Importieren Sie auf HCS1 die Datenpakete, um den Daten Cache vorab zu laden.

4. Konfigurieren Sie auf DC1 in die Domäne eingebundener Zweigstellen Client Computer für den gehosteten Cache Modus, indem Sie Gruppenrichtlinie mit BranchCache-Richtlinien Einstellungen konfigurieren.

5. Aktualisieren Sie auf Client Computern Gruppenrichtlinie.

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Bereitstellungs Planung für den BranchCache-gehosteten Cache Modus](3-Bc-Hcm-Plan.md).