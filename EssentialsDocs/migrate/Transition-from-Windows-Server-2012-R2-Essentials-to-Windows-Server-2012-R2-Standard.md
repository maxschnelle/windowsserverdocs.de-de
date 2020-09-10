---
title: Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: a60ffd7593da8e8275e36e9aec2cf6e25fbe23db
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625306"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server 2016 ist das für die Cloud geeignete Betriebssystem, das Ihre aktuellen Workloads unterstützt, während neue Technologien eingeführt werden, die den Übergang zu Cloud Computing erleichtern. Der Inhalt von Windows Server 2016 hilft Ihnen, Sie bereit zu machen.

 Windows Server Essentials unterstützt bis zu 25 Benutzer und 50 Geräte. Wenn Ihr Geschäftsbedarf den Grenzwert überschreitet, können Sie eine direkte Lizenz Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard durchführen, um die Lizenz Konformität zu gewährleisten.

 Nach der Umstellung auf Windows Server 2012 R2 Standard werden die Benutzerkonten-und Geräte Limits entfernt, aber die Features, die für Windows Server Essentials eindeutig sind (z. b. das Dashboard, die Remote Webzugriff und die Client Computer Sicherung), bleiben weiterhin verfügbar. Aufgrund technischer Einschränkungen für diese Funktionen werden jedoch höchstens 100 Benutzerkonten und 200 Geräte unterstützt. Die Sicherungsfunktion für Clientcomputer wird die Sicherung von bis zu 75 Geräten unterstützen.

> [!IMPORTANT]
>   Windows Server 2012 R2 Standard erfordert eine Client Zugriffslizenz (Client Access License, CAL) für jeden Benutzer bzw. jedes Gerät in Ihrer Umgebung. Dies unterscheidet sich von Windows Server Essentials, bei dem das CAL-Modell nicht verwendet wird und keine CALs vorhanden sind. Wenn Sie von Windows Server Essentials zu Windows Server 2012 R2 Standard wechseln, müssen Sie die entsprechende Anzahl und Art von CALs für Ihre Umgebung erwerben (die meisten Kunden erwerben Benutzer-CALs).

## <a name="before-the-transition"></a>Vor der Umstellung

-   Vor der Umstellung von Windows Server Essentials auf Windows Server 2012 R2 Standard sollten Sie die Server Daten vollständig sichern.

    > [!IMPORTANT]
    >  Ohne eine vollständige Sicherung des Servers kann der Zustand des Servers vor der Umstellung nicht wiederhergestellt werden.

-   Außerdem sollten Sie sicherstellen, dass Sie den Endbenutzer-Lizenzvertrag (EULA) für Windows Server 2012 R2 Standard lesen und verstehen. So zeigen Sie die EULA an:

    1.  Öffnen Sie ein Befehlsfenster als Administrator.

    2.  Führen Sie den folgenden Befehl aus:

         **dism /online /set-edition:ServerStandard /geteula:** *eula path* (wobei *eula path* für den Speicherort steht, an dem die EULA-Datei gespeichert werden soll. Beispiel: C:\ws8std_eula.rtf). Achten Sie darauf, RTF als Dateierweiterung zu verwenden.

    3.  Navigieren Sie zum Speicherort der Datei, und doppelklicken Sie darauf, um sie zu öffnen.

## <a name="transition-to--windows-server-2012-r2-standard"></a>Umstellung auf Windows Server 2012 R2 Standard
 Nachdem Sie beschlossen haben, von Windows Server Essentials zu Windows Server 2012 R2 Standard zu wechseln, führen Sie die folgenden beiden Schritte aus:

1. Erwerben Sie eine Lizenz für Windows Server 2012 R2 Standard und die entsprechende Anzahl von Benutzer-und/oder Geräte-Client Zugriffs Lizenzen für Ihre Umgebung.

    Sie können eine Lizenz für Windows Server 2012 R2 Standard von einem Einzelhandelsunternehmen, einem Verteiler oder mit der Hilfe eines [Microsoft-Partners](https://pinpoint.microsoft.com/SelectCulture.aspx)erwerben.

   > [!NOTE]
   >  Wenn Sie anfänglich Windows Server 2012 R2 Standard erworben haben und Ihre Downgrade-Rechte zum Installieren einer ihrer beiden virtuellen Instanzen als Windows Server Essentials übernommen haben, müssen Sie keine zusätzlichen Schritte erwerben.
   >
   >  Wenn Sie Windows Server 2012 R2 Standard über den Volumenlizenz Kanal erwerben, können Sie ein ISO-Abbild und ein Product Key für Windows Server 2012 R2 Standard aus dem Volume Licensing Service Center (VLSC) herunterladen.
   >
   >  Wenn Sie Windows Server 2012 R2 Standard über einen anderen Kanal erwerben, können Sie ein ISO-Abbild und eine Evaluierungs Product Key für Windows Server Essentials aus dem [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)herunterladen. Durch das Ausführen der Umstellung gemäß der Beschreibung im folgenden Schritt wird das Evaluierungsprodukt in ein vollständig lizenziertes und unterstütztes Produkt umgewandelt.

2. Öffnen Sie Windows PowerShell als Administrator, und führen Sie dann den folgenden Befehl aus:

    **dismus/Online/Set-Edition: Server Standard/AcceptEULA/ProductKey:** *Product Key* (wobei *Product Key* der Product Key für Ihre Kopie von Windows Server 2012 R2 Standard ist).

    Der Server wird neu gestartet, um den Umstellungsprozess fertigzustellen.

   Nach dem Übergang verbleiben die Windows Server Essentials-Features auf dem Server und werden von bis zu 100 Benutzern und 200 Geräten unterstützt.

## <a name="additional-references"></a>Weitere Verweise


-   [Migrieren von Serverdaten zu Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

