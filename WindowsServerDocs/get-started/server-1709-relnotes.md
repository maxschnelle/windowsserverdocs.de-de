---
title: 'Anmerkungen zu dieser Version: Wichtige Probleme in Windows Server, Version 1709'
description: Nachfolgend sind wichtige Probleme aufgeführt, für die eine Problemumgehung erforderlich ist, um einen Absturz, das Aufhängen des Systems, einen Installationsfehler oder Datenverlust zu verhindern.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 04/23/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4eebc498289a81c7f27fcf4b84d81ae13bc38e4f
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63688248"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>Versionshinweise: Wichtige Probleme in Windows Server, Version 1709

>Gilt für: Windows Server (Semi-Annual Channel)

In diesen Anmerkungen zur Version sind die wichtigsten Probleme im Betriebssystem Windows Server&reg; zusammengefasst, und Sie erfahren, wie Sie diese Probleme gegebenenfalls umgehen können. Informationen zu standardmäßigen Änderungen, neuen Features und Fixes in diesem Release finden Sie unter [Neues in Windows Server, Version 1709](whats-new-in-windows-server-1709.md) und in den Ankündigungen der zuständigen Featureteams. Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server 2016.  

Dieses Dokument wird ständig aktualisiert. Wenn kritische Probleme ermittelt werden, die eine Problemumgehung erfordern, werden diese genauso wie neue Problemumgehungen und Fixes hinzugefügt, sobald sie verfügbar sind.  
  
## <a name="storage-spaces-direct"></a>Direkte Speicherplätze
[comment]: # (ID: unknown; Submitter: stevenek; state: signed off)  
„Direkte Speicherplätze“ ist in Windows Server, Version 1709 nicht enthalten. Wenn Sie *Enable-ClusterStorageSpacesDirect* oder dessen Alias *Enable-ClusterS2D* auf einem Server unter Windows Server, Version 1709, aufrufen, wird die Fehlermeldung „Der angeforderte Vorgang wird nicht unterstützt“ angezeigt.

Das Einführen von Servern mit Windows Server, Version 1709, auf einer Windows Server 2016-Bereitstellung mit direkten Speicherplätzen wird auch nicht unterstützt.

Das Windows Server-Releasemodell bietet eine neue Option zur Angleichung an ähnliche Release- und Servicemodelle für [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) und [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US). Die Releases des halbjährigen Kanals bieten neuen Funktionen für Kunden, die einen schnellen Rhythmus des Verschiebens benötigen, und bietet zwei neue Releases pro im Jahr: im Frühling und im Herbst.

Der halbjährliche Kanal von Windows Server konzentriert sich auf Container- und Anwendungsszenarien, die von schnelleren Innovationen profitieren. Weitere Informationen finden Sie in diesem [Blog](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update). Kunden, die für nach Infrastrukturrollen wie „Direkte Speicherplätze“ suchen, sollten die Releases des Long-Term Servicing Channel verwenden, z.B. Windows Server 2016 (jetzt verfügbar) und [Windows Server-2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (später in diesem Jahr verfügbar). Wir setzen uns für die Entwicklung der besten Plattform für hyperkonvergente Infrastruktur ein und entwickeln ständig neue Features und verbessern vorhandene basierend auf Ihrem Feedback. 

„Direkte Speicherplätze“ wurde in Windows Server 2016 eingeführt und ist die Grundlage für unsere hyperkonvergente Plattform. Wir haben uns über die positive Übernahme der hyperkonvergenten Microsoft-Plattform sehr gefreut, und wir engagieren uns für unsere Kunden.

Wir haben Ihr Feedback berücksichtigt und arbeiten an der Bereitstellung der [nächsten Gruppe von Innovationen](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) für unsere hyperkonvergente Plattform. Diese Features stehen noch heute in den [Windows-Insider](https://insider.windows.com/for-business/)-Builds zur Verfügung, und wir würden uns freuen, wenn Sie diese ausprobieren und uns Ihr Feedback mitteilen. Kunden, die nach einer überprüften hyperkonvergenten Lösung suchen, empfehlen wir das Programm [Windows Server Software Defined](http://microsoft.com/wssd).
