---
title: Entfernte oder für den Austausch geplante Features ab Windows Server (Version 1709)
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
ms.openlocfilehash: 37970f3bee2070cffc77bff855a8f28641196b24
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66452861"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1709"></a>Entfernte oder für den Austausch geplante Features ab Windows Server (Version 1709)

>Gilt für: Windows Server, Version 1709

Die folgende Liste enthält Features und Funktionen der Version 1709 von Windows Server, die entweder in diesem Release aus dem Produkt entfernt wurden oder potenziell in künftigen Releases ersetzt werden. Sie ist für IT-Experten vorgesehen, die Betriebssysteme in einer kommerziellen Umgebung aktualisieren. **Für diese Liste sind Änderungen in zukünftigen Releases vorbehalten. Zudem enthält sie möglicherweise nicht alle betroffenen Features oder Funktionen.** 

## <a name="features-removed-from-windows-server-version-1709"></a>Aus Windows Server (Version 1709) entfernte Features
Die Version 1709 von Windows Server enthält die gleichen Features wie Windows Server 2016. Dieses Release bietet allerdings andere Installationsoptionen als Windows Server 2016:

- Als Release des halbjährlichen Kanals steht für die Version 1709 von Windows Server nur die Server Core-Installationsoption zur Verfügung. Ausführliche Informationen findest du unter [Windows Server-Wartungskanäle: LTSC und SAC](../get-started-19/servicing-channels-19.md).
- Ab diesem Release steht Nano Server nicht mehr als installierbares Hostbetriebssystem zur Verfügung. Stattdessen ist Nano Server als Containerbetriebssystem verfügbar. Weitere Informationen findest du unter [Changes to Nano Server in Windows Server Semi-Annual Channel](nano-in-semi-annual-channel.md) (Änderungen für Nano Server in Windows Server (halbjährlicher Kanal)).
- Ab diesem Release wird die Version 1 von Server Message Block (SMB) standardmäßig nicht mehr installiert. Ausführliche Informationen findest du unter [SMBv1 wird für die Versionen Windows 10 Fall Creators Update und Windows Server, Version 1709 und höher, standardmäßig nicht installiert.](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows).


## <a name="features-being-considered-for-replacement-starting-with-subsequent-releases"></a>Features, die in späteren Releases möglicherweise ersetzt werden

Die folgenden Features und Funktionen werden möglicherweise in Releases nach der Version 1709 von Windows Server ersetzt. Sie werden später ggf. vollständig aus dem installierten Produktimage entfernt und durch andere Features oder Funktionen ersetzt (oder können aus anderen Quellen installiert werden). In diesem Release sind sie allerdings weiterhin verfügbar, wenn auch bisweilen mit geringerem Funktionsumfang. Bereite dich bei Anwendungen, Code und Szenarien, die auf diese Features angewiesen sind, möglichst schon jetzt auf den Einsatz alternativer Methoden oder auf den zukünftigen Austausch vor.

Feedback zum vorgeschlagenen Austausch dieser Features kannst du über die [Feedback-Hub-App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) abgeben. Diese App wird zwar unter Windows 10 ausgeführt, du kannst uns damit aber auch Feedback zu Windows Server sowie zur Dokumentation senden.

### <a name="iis-6-management-compatibility"></a>IIS 6-Verwaltungskompatibilität
Für folgende Features wird ein Austausch in Betracht gezogen:

- IIS 6-Metabasiskompatibilität (Web-Metabase)
- IIS 6-Verwaltungskonsole (Web-Lgcy-Mgmt-Console)
- IIS 6-Skriptingtools (Web-Lgcy-Scripting)
- IIS 6-WMI-Kompatibilität (Web-WMI)

Anstelle der IIS 6-Metabasiskompatibilität (fungiert als Emulationsebene zwischen IIS 6-basierten Metabasisskripts und der dateibasierten Konfiguration, die von IIS 7 oder neueren Versionen verwendet wird) solltest du Verwaltungsskripts migrieren, um die dateibasierte IIS-Konfiguration direkt zu verwenden – etwa mithilfe von Tools wie dem Microsoft.Web.Administration-Namespace.

Außerdem solltest du von IIS 6.0 oder älteren Versionen zur neuesten Version von IIS migrieren, die jeweils in der aktuellen Version von Windows Server zur Verfügung steht.


### <a name="iis-digest-authentication"></a>IIS-Digestauthentifizierung
Diese Authentifizierungsmethode wird voraussichtlich ersetzt. Beginne stattdessen mit der Verwendung anderer Authentifizierungsmethoden wie etwa der Clientzertifikatszuordnung (siehe [Configuring One-to-One Client Certificate Mappings](https://docs.microsoft.com/iis/manage/configuring-security/configuring-one-to-one-client-certificate-mappings) (Konfigurieren der 1:1-Clientzertifikatzuordnung) oder der Windows-Authentifizierung (siehe [Application Settings (appsettings.json)](https://docs.microsoft.com/iis-administration/configuration/appsettings.json) (Anwendungseinstellungen (appsettings.json)).

### <a name="internet-storage-name-service-isns"></a>iSNS (Internet Storage Name Service)
iSNS wird möglicherweise ersetzt. Das SMB-Feature (Server Message Block) bietet im Wesentlichen die gleichen Funktionen sowie zusätzliche Features. Hintergrundinformationen zu diesem Feature findest du in der [Übersicht über Server Message Block](https://technet.microsoft.com/library/hh831795(v=ws.11).aspx).

### <a name="rsaaes-encryption-for-iis"></a>RSA/AES-Verschlüsselung für IIS 
Diese Verschlüsselungsmethode wird möglicherweise ersetzt, da die bessere CNG-Methode (Cryptography API: Next Generation) bereits verfügbar ist. Weitere Informationen zur CNG-Verschlüsselung findest du in der [Übersicht über CNG](https://msdn.microsoft.com/library/windows/desktop/aa375276(v=vs.85).aspx).

### <a name="windows-powershell-20"></a>Windows PowerShell 2.0
Für diese frühe Version von Windows PowerShell stehen bereits mehrere neuere Versionen zur Verfügung. Migriere zu Windows PowerShell 5.0 oder einer höheren Version, um die besten Features und die beste Leistung zu erhalten. Weitere Informationen findest du in der [PowerShell-Dokumentation](https://docs.microsoft.com/powershell/index?view=powershell-5.1).

