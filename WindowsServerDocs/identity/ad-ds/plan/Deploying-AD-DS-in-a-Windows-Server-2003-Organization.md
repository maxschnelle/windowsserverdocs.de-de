---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Bereitstellen von AD DS in einer Windows Server 2003-Organisation
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 2eed366cfa6c27fd444236b924537d34fb11698d
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069342"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Bereitstellen von AD DS in einer Windows Server 2003-Organisation

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn in Ihrem Unternehmen derzeit Windows Server 2003 Active Directory ausgeführt wird, können Sie Windows Server 2008 Active Directory Domain Services (AD DS) bereitstellen, indem Sie entweder ein direktes Upgrade einiger oder aller ihrer Betriebssysteme der Domänen Controller auf Windows Server 2008 durchführen oder Domänen Controller unter Windows Server 2008 in Ihre Umgebung einführen.

Bevor Sie einen Domänen Controller, auf dem Windows Server 2008 ausgeführt wird, zu einer vorhandenen Windows Server 2003 Active Directory-Domäne hinzufügen können, müssen Sie **adprep** ausführen, ein Befehlszeilen Tool. Adprep erweitert das AD DS Schema, aktualisiert die Standard Sicherheits Beschreibungen ausgewählter Objekte und fügt die von einigen Anwendungen benötigten neuen Verzeichnisobjekte hinzu. Adprep ist auf dem Installations Datenträger für Windows Server 2008 (\sources\adprep\adprep.exe) verfügbar. Weitere Informationen finden Sie unter [adprep](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731728(v=ws.11)).

In der folgenden Abbildung werden die Schritte zum Bereitstellen von Windows Server 2008 AD DS in einer Netzwerkumgebung gezeigt, in der derzeit Windows Server 2003 Active Directory ausgeführt wird.

![Bereitstellen in einer Windows 2003-Organisation](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)

> [!NOTE]
> Wenn Sie die Domänen-oder Gesamtstruktur Funktionsebene auf Windows Server 2008 festlegen möchten, müssen alle Domänen Controller in Ihrer Umgebung das Betriebssystem Windows Server 2008 ausführen.

Zum Konsolidieren von Ressourcen Domänen und Konto Domänen, die von einer Windows Server 2003-Umgebung im Rahmen ihrer Windows Server 2008-AD DS Bereitstellung aktualisiert werden, ist möglicherweise eine Gesamtstruktur-oder Gesamtstruktur übergreifende Domänen Umstrukturierung erforderlich Durch die Umstrukturierung AD DS Domänen zwischen Gesamtstrukturen können Sie die Komplexität der Darstellung Ihrer Organisation in AD DS verringern und so die damit verbundenen Verwaltungskosten senken. Durch die Umstrukturierung AD DS Domänen in einer Gesamtstruktur können Sie den Verwaltungsaufwand für Ihre Organisation verringern, indem Sie den Replikations Datenverkehr verringern, die erforderliche Menge an Benutzer-und Gruppenverwaltung reduzieren und die Verwaltung von Gruppenrichtlinie vereinfachen. Weitere Informationen finden Sie unter [ADMT Guide: Migrieren und umstrukturieren von Active Directory Domänen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Eine Liste der detaillierten Aufgaben, die Sie zum Planen und Bereitstellen von AD DS in einer Organisation mit Windows Server 2003 Active Directory ausführen können, finden Sie unter Prüfliste: Bereitstellen von [AD DS in einer Windows Server 2003-Organisation](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771407(v=ws.10)).
