---
title: In Windows Server (Version 1709) entfernte oder veraltete Features
description: Features und Funktionen, die entfernt wurden bzw. deren Entfernung aus künftigen Versionen geplant ist.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 06/05/2018
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 28f6393d57daaa04c15aa7c56dacc2c4d65dc2a3
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976744"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1709"></a>Entfernte oder für den Austausch geplante Features ab Windows Server Version 1709

>Gilt für: Windows Server, Version 1709

Es folgt eine Liste der Features und Funktionen der Version 1709 von Windows Server die für diese Version aus dem Produkt entfernt wurden oder möglicherweise in künftigen Versionen potenziell entfernt werden („veraltet“). Sie ist für IT-Experten vorgesehen, die Betriebssysteme in einer kommerziellen Umgebung aktualisieren. **Diese Liste unterliegt in künftigen Versionen und enthalten möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-removed-from-windows-server-version-1709"></a>Aus der Version 1709 von Windows Server entfernte Features
Die Version 1709 von Windows Server enthält die gleichen Features, die in Windows Server 2016 enthalten sind. Diese Version bietet allerdings verschiedene Installationsoptionen als die von Windows Server 2016:

- Als Veröffentlichung des halbjährigen Kanals bietet die Version 1709 von Windows Server nur die Server Core-Installationsoption an. Weitere Informationen finden Sie unter [Vergleich wartungskanälen](..\get-started-19\servicing-channels-19.md).
- Ab dieser Version steht Nano Server nicht als ein installierbares Host-Betriebssystem zur Verfügung. Nano Server ist stattdessen als Containerbetriebssystem verfügbar. Weitere Informationen finden Sie unter [Änderungen in Nano Server in der Version 1709 von Windows Server](nano-in-semi-annual-channel.md).
- Ab dieser Version, wird Version 1 von Server Message Block (SMB) nicht mehr standardmäßig installiert. Weitere Informationen finden Sie unter [SMBv1 ist standardmäßig in Windows 10 Fall Creators Update und Windows Server, Version 1709 und höher nicht installiert](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows).


## <a name="features-being-considered-for-replacement-starting-with-subsequent-releases"></a>Features, die für den Austausch nachfolgender Versionen berücksichtigt werden

Die folgenden Features und Funktionen werden für den Austausch in den Versionen nach der Version 1709 in Windows Server in Betracht gezogen. Zu einem späteren Zeitpunkt werden sie vollständig aus dem installierten Produktbild entfernt und von anderen Features oder Funktionen ersetzt (oder sie sind aus anderen Quellen installierbar). Sie sind allerdings noch in dieser Version verfügbar, auch wenn manchmal bestimmte Funktionen daraus entfernt werden. Beginnen Sie jetzt mit der Planung des Einsatzes alternativer Methoden oder zukünftiger Ersetzungen für Anwendungen, Code oder Nutzungsarten, die von diesen Features abhängen.

Wenn Sie Feedback über die vorgeschlagenen Ersetzung dieser Features haben, können Sie dieses mithilfe der [Feedback-Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) abgeben. Obwohl diese App auf Windows 10 ausgeführt wird, können Sie uns ebenfalls Feedback zu Windows Server-Produkten (und der Dokumentation) senden.

### <a name="iis-6-management-compatibility"></a>IIS 6-Verwaltungskompatibilität:
Bestimmte Funktionen, die für den Austausch berücksichtigt werden, sind:

- IIS 6-Metabasiskompatibilität (Web-Metabasis)
- IIS 6-Verwaltungskonsole (Web-Lgcy-Mgmt-Konsole)
- IIS 6-Skripting-Tools (Web-Lgcy-Skripting)
- IIS 6-WMI-Kompatibilität (Web-WMI)

Anstelle der IIS 6-Metabasiskompatibilität (fungiert als Emulationsebene zwischen IIS 6-basierten Metabasisskripts und den Datei-basierten Konfiguration, die von IIS 7 oder neueren Versionen verwendet werden) sollten Sie zunächst Verwaltungsskripts migrieren, um IIS-dateibasierte Konfiguration mithilfe von Tools wie z. B. die Microsoft.Web.Administration-Namespace direkt anzuzielen.

Sie sollten auch die Migration von IIS 6.0 oder früheren Versionen starten und auf die neueste Version von IIS migrieren, die immer in der neuesten Version von Windows Server verfügbar ist.


### <a name="iis-digest-authentication"></a>IIS-Digestauthentifizierung
Diese Authentifizierungsmethode ist für den Austausch geplant. Beginnen Sie stattdessen, andere Authentifizierungsmethoden wie z. B. Clientzertifikate (diese finden Sie unter [1: 1-Clientzertifikatzuordnung konfigurieren](https://docs.microsoft.com/iis/manage/configuring-security/configuring-one-to-one-client-certificate-mappings)) oder Windows-Authentifizierung (diese finden Sie unter [Anwendungseinstellungen](https://docs.microsoft.com/iis-administration/configuration/appsettings.json)) zu verwenden.

### <a name="internet-storage-name-service-isns"></a>iSNS (Internet Storage Name Service)
iSNS wird für den Austausch berücksichtigt. Das Server Message Block (SMB)-Feature bietet im Wesentlichen die gleiche Funktionalität mit weiteren Features. Weitere Hintergrundinformationen zu den Funktionen finden Sie unter [Server Message Block – Übersicht](https://technet.microsoft.com/library/hh831795(v=ws.11).aspx).

### <a name="rsaaes-encryption-for-iis"></a>RSA/AES-Verschlüsselung für IIS 
Diese Verschlüsselungsmethode wird für den Austausch angesehen werden, da die überlegene Cryptography API: Next Generation (CNG)-Methode ist bereits verfügbar. Weitere Informationen zur CNG-Verschlüsselung finden Sie unter [Übersicht über CNG](https://msdn.microsoft.com/library/windows/desktop/aa375276(v=vs.85).aspx).

### <a name="windows-powershell-20"></a>Windows PowerShell 2.0
Diese frühe Version von Windows PowerShell wurde durch mehrere neueren Versionen ersetzt. Migrieren Sie für die besten Features und Leistungen auf Windows PowerShell 5.0 oder höher. Weitere Informationen finden Sie unter [PowerShell-Dokumentation](https://docs.microsoft.com/powershell/index?view=powershell-5.1).

