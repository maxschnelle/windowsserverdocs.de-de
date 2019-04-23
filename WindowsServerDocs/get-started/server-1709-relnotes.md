---
title: Anmerkungen zu dieser Version – Wichtige Probleme in Windows Server, Version 1709
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861981"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>Versionshinweise: Wichtige Probleme in Windows Server, Version 1709

>Gilt für: Windows Server (Semi-Annual Channel)

In diesen Anmerkungen zur Version sind die wichtigsten Probleme im Betriebssystem Windows Server&reg; zusammengefasst, und Sie erfahren, wie Sie diese Probleme gegebenenfalls umgehen können. Informationen zu standardmäßigen Änderungen, neuen Features und Fixes in diesem Release finden Sie unter [Neues in Windows Server, Version 1709](whats-new-in-windows-server-1709.md) und in den Ankündigungen der zuständigen Featureteams. Sofern es nicht anders angegeben ist, gelten alle aufgeführten Probleme für alle Editionen und Installationsoptionen von Windows Server 2016.  

Dieses Dokument wird ständig aktualisiert. Wenn kritische Probleme ermittelt werden, die eine Problemumgehung erfordern, werden diese genauso wie neue Problemumgehungen und Fixes hinzugefügt, sobald sie verfügbar sind.  
  
## <a name="storage-spaces-direct"></a>Direkte Speicherplätze
[comment]: # (ID: Unbekannter; Übermittler: Stevenek; Status: hat genehmigt)  
„Direkte Speicherplätze“ ist in Windows Server, Version 1709 nicht enthalten. Wenn Sie *Enable-ClusterStorageSpacesDirect* oder dessen Alias *Enable-ClusterS2D* auf einem Server unter Windows Server, Version 1709, aufrufen, wird die Fehlermeldung "Der angeforderte Vorgang wird nicht unterstützt" angezeigt.

Das Einführen von Servern mit Windows Server, Version 1709, auf einer Windows Server 2016-Bereitstellung mit direkten Speicherplätzen wird auch nicht unterstützt.

Das Modell der Windows Server-Version bietet eine neue Option zur Angleichung an ähnliche Veröffentlichungs- und Wartungsmodelle für [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) und [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US). Die Veröffentlichung des halbjährigen Kanals bieten neuen Funktionen für Kunden, die einen schnellen Rhythmus des Verschiebens benötigen, und bietet zwei neue Versionen pro im Jahr: im Frühling und im Herbst.

Halbjährlicher Kanal von Windows Server konzentriert sich auf Container und Anwendungsszenarien, die von schnelleren Innovationen profitieren, finden Sie in diesem [Blog](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update) für zusätzliche Informationen. Kunden, die für die Infrastrukturrollen, beispielsweise "direkte Speicherplätze", sollten die Long-term Servicing Versionen wie Windows Server 2016 (jetzt verfügbar) verwenden und [Windows Server-2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (später in diesem Jahr verfügbar). Es wird ein Commit für die Erstellung der besten Plattform für die hyperkonvergenten Infrastruktur ausgeführt, und wir weiterhin neue Features entwickeln und verbessern vorhandene basierend auf Ihrem Feedback. 

"Direkte Speicherplätze" wurde in Windows Server 2016 eingeführt und ist die Grundlage für unsere zusammengeführte Plattform. Wir haben uns über die positive Übernahme der zusammengeführten Microsoft-Plattform sehr gefreut, und wir engagieren uns für unsere Kunden.

Wir haben Ihr Feedback umgesetzt und zum Übermitteln von arbeiten die [nächsten Satz von Innovationen](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) für unsere Plattform hyper-konvergiert. Diese Funktionen stehen heute in [Windows Insider](https://insider.windows.com/for-business/) Builds, und wir würden uns freuen, ausprobieren und uns Ihr Feedback. Für Kunden, die nach einer überprüften zusammengeführten Lösung suchen, empfehlen wir das [Windows Server-Software-Defined](http://microsoft.com/wssd)-Programm.
