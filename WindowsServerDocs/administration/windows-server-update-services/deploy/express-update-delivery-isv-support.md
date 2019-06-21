---
title: ISV-Unterstützung für Express-Updatebereitstellung
description: Windows Server Update Service (WSUS)-Thema – wie Hersteller ISVS (Independent Software) kann Express-Update-Bereitstellung mithilfe von WSUS konfigurieren.
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 5f2a99bb69fd41c05013788187838f8fceb5f69a
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280453"
---
# <a name="express-update-delivery-isv-support"></a>ISV-Unterstützung für Express-Updatebereitstellung

>Gilt für: Windows 10, WindowsServer 2016

Windows 10-Update-Downloads können groß sein, da jedes Paket auf alle zuvor veröffentlichten Updates, um sicherzustellen, dass Konsistenz und Einfachheit enthält.  

Version 7, Windows seit verringern, die Größe des Windows Update-Downloads durch eine Funktion namens [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2), und obwohl Geräte für Verbraucher standardmäßig unterstützt, wird Windows 10 Enterprise-Geräte erfordern Windows Server Update Services (WSUS) Express nutzen.

## <a name="how-microsoft-supports-express"></a>Wie Microsoft Express unterstützt

- **Express auf dem WSUS-eigenständiger**

    Übermittlung von Express-Update ist bereits [verfügbar auf allen unterstützten Versionen von WSUS](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx).

- **Auf Geräten, die direkt mit Windows Update verbunden Express** 

    Geräte für Verbraucher Unterstützung von Express-Download: sie verwenden den Windows Update (WU)-Client zu überprüfen, herunterladen und Installieren von Updates. Während der Downloadphase des WU-Clients Anforderungen von Express-Pakete und lädt die entsprechende Bytebereiche.

-  **Enterprise-Geräte, die mit [Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** verwendet werden, profitieren ebenfalls von der Unterstützung der Express-Updatebereitstellung ohne Änderung der Konfiguration.

## <a name="how-isvs-can-take-advantage-of-express"></a>Wie können ISVs Express nutzen

ISVs können WSUS und WU-Clients zur Unterstützung von Express-Update-Bereitstellung verwenden. Microsoft empfiehlt die folgenden drei Schritte, die in den folgenden Abschnitten ausführlicher erläutert:

1.  [**Konfigurieren von WSUS**](#BKMK_1)

    WSUS-Server ist erforderlich, damit überprüfen und die Möglichkeit, updatesynchronisierungen (Weitere Informationen finden Sie [hier](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx))

2.  [**Geben Sie ein, und füllen Sie einen ISV-Datei-cache**](#BKMK_2)

    Ein ISV-Dateicache wird empfohlen, zum Hosten des Update-Inhalts, die die CAB-Updatedateien (.cab-Dateien) enthält, und die Express-Pakete (.psf-Dateien).

3.  [**Richten Sie einen ISV-Client-Agent so Vorgängen des WU-Clients**](#BKMK_3)

>[!NOTE]
>Erfordert Kumulatives Update für Windows 10 Version 1607 Release in (oder nach) Januar 2017 ([KB3213986 (OS Build 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693) installiert werden.
    
   - Der ISV-Client-Agent bestimmt, welche updates genehmigen, und wenn herunterladen und Installieren der updates
   - Die WU-Clients bestimmt die Bytebereiche zum Herunterladen und initiiert die downloadanforderung

### <a name="BKMK_1"></a>Schritt 1: Konfigurieren von WSUS

WSUS dient als Schnittstelle zu Windows Update und verwaltet alle Metadaten, die Beschreibung von Express-Pakete, die heruntergeladen werden müssen. Wenn Sie bereitstellen möchten, finden Sie unter [ **Übersicht über die von Windows Server Update Services 3.0 SP2**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx). Sobald WSUS bereitgestellt wurde, ist der wichtigste Aspekt, ob Inhalt aktualisieren lokal auf dem WSUS-Server zu speichern. Wenn Sie WSUS konfigurieren zu können, wird empfohlen, keine Updates lokal speichern. Dies setzt voraus, dass Sie bereits über Software, die Bereitstellung dieser Pakete in Ihrer Umgebung weitergeleitet haben. Weitere Informationen zum Konfigurieren des lokalen WSUS-Speichers finden Sie unter [ **Bestimmen des Installationsorts für Store-Updates**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx).

### <a name="BKMK_2"></a>Schritt 2: Geben Sie ein, und füllen Sie den ISV-Dateicache 

#### <a name="specify-the-isv-file-cache"></a>Geben Sie den ISV-Dateicache

Neue clientseitige Gruppenrichtlinien und Internet-Informationsdienste (Mobile Device Management, MDM) Einstellungen finden Sie unter den [ **Konfigurationsdienstanbieter-Referenz** ](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) definieren Sie den Speicherort des Dateicaches ISV.

| **Name**                                              | **Beschreibung**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Konfigurieren von einem alternativen Downloadspeicherort für Updates. | Gibt einen alternativen Intranetdienst-Server als Host für Updates von Microsoft Update an. Klicken Sie dann können dieses Update-Dienst Sie Computer in Ihrem Netzwerk automatisch aktualisieren |

Es gibt zwei Optionen beim Einrichten der alternativen Downloadspeicherort für den ISV-Datei-Cache:

1. **Geben Sie einen ISV-HTTP-Hostnamen des Synchronisierungsservers**, d.h., dass der ISV-Datei-Cache
    
    Dieser Ansatz wird konfiguriert, das WU-Clients, um Anforderungen an den HTTP-Server in der Richtlinie angegebenen herunterladen zu machen

2. **Geben Sie "localhost"**
 
    Dieser Ansatz konfiguriert die WU-Clients, um Anforderungen auf "localhost" herunterladen zu machen. Dadurch wird den ISV-Client-Agent, um diese Anforderungen und die Route nach Bedarf zur Verarbeitung der downloadanforderung zu verarbeiten.

> [!IMPORTANT]
> Der ISV-Datei-Cache ist Folgendes erforderlich:                                                          
> - Der Server muss über HTTP 1.1-gemäß der RFC kompatibel sein: <http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> Insbesondere benötigt, um der Webserver zu unterstützen                                                                                                                                                                                                                                       [ **HEAD** ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) und [ **erhalten** ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) Anforderungen<br>                                                                                                                                                                                                                                                                                                  -Teilweise Anforderungen<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   Keep-alive-<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -Verwenden Sie nicht "Transfer-Encoding: chunked"                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>Füllen Sie den ISV-Datei-Cache

Der ISV-Datei-Cache muss aktualisiert werden, mit Dateien im Zusammenhang mit den Updates auf verwalteten Clients installiert werden. 

**Der ISV-Datei-Cache zu füllen:**

1. Verwendung [WSUS-APIs](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx) den Zugriff auf des Updates Dateipfad und Dateinamen für den MU-Dienst.

    Die Metadaten für die einzelnen Updates auf WSUS-Server enthält des Updates Pfad und Dateinamen auf Microsoft Update wie folgt (Microsoft Update-Hostnamen in fettformatierung, gefolgt vom Pfad und Dateiname): **<http://download.windowsupdate.com>** /c/Msdownload/Update / Software/UPDT/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74.msu

2. Herunterladen von Dateien von Microsoft Update, und speichern Sie sie in der ISV-Datei-Cache mit einer dieser beiden Methoden: 

   - Store-Dateien, die mithilfe der **gleichen Ordnerpfad als für den Dienst MU**

   - Store-Dateien, die mit einem **ISV definierten Ordnerpfad**

     HTTP-Umleitung für Server (oder "localhost") haben **HTTP GET** -Anforderungen, die den MU Ordnernamen Pfad und Dateinamen ein, um den Speicherort der ISV zu verweisen.

### <a name="BKMK_3"></a>Schritt 3: Richten Sie einen ISV-Client-Agent so Vorgängen des WU-Clients

Der ISV-Client-Agent orchestriert den Download und die Installation genehmigter Updates, die mit den folgenden empfohlenen Workflow:

1.  Der ISV-Client-Agent Ruft die WU-Clients auf dem WSUS-Server überprüfen

2.  Die Überprüfung gibt den Satz der anwendbaren Updates an den Windows Update-client

3.  Der ISV-Client bestimmt, welche updates genehmigen, herunterladen und installieren

4.  Der ISV-Client-Agent ruft WU-Clients zum Herunterladen der genehmigten updates

5.  Sobald die Updates heruntergeladen wurden, ruft der ISV-Client-Agent die WU-Clients, um die genehmigten Updates installieren

Finden Sie unter [suchen, herunterladen und Installieren von Updates](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx) Weitere Informationen zur Verwendung des WU-Clients überprüfen, Updates herunterladen und installieren.

### <a name="download-workflow-options"></a>Workflow-Downloadoptionen

Es folgen zwei Abbildungen von Optionen zum Herunterladen von Workflow von einem ISV-Datei-Cache:

![Workflow 1](../../media/express-update-delivery-isv-support/image1.png)

![Workflow 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Wie der Express-Download funktioniert

- Für Betriebssystemupdates, die Express unterstützen, sind zwei Versionen der Dateinutzlast im Dienst gespeichert:

  - **Vollversion** – im Wesentlichen und Ersetzen Sie dabei die lokalen Versionen von die Updatebinärdateien

  - **Express-Version** – zum Patchen der vorhandenen Binärdateien auf dem Gerät benötigt, die die Deltas enthält. 

    Sowohl die vollständige Version und der Express-Version werden in den Updatemetadaten verwiesen, die als Teil der Phase der Überprüfung an den Client heruntergeladen wurde. 

    **Express-Download funktioniert wie folgt aus:**

    Der WU-Client versucht Express zuerst in bestimmten Situationen Herbst zurück zum vollständigen Dateien herunterladen und bei Bedarf (z. B. wenn über einen Proxy, der Anforderungen für Bytebereiche unterstützt).

  1. Wenn die WU-Clients einen Express-Download initiiert **des WU-Clients zuerst lädt einen Stub**, diese ist Teil des Express-Pakets.

  2. **Die WU-Clients übergibt dieser Stub für dem Windows Installer**, verwendet den Stub möchten eine lokale Inventur, vergleichen die Deltas aus der Datei auf dem Gerät mit, was benötigt wird, um auf die neueste Version der Datei Angeboten zu erhalten.

  3. Die **Windows Installer fordert anschließend die WU-Clients zum Herunterladen der Bereiche** erforderlich ermittelt wurde.

  4. **Der Windows Update-Client lädt diese Bereiche und übergibt sie an dem Windows Installer**, die die Bereichen angewendet und bestimmt, ob es sich bei zusätzliche Bereichen erforderlich sind. Dies wird wiederholt, bis der Windows Installer des WU-Clients teilt mit, dass alle erforderlichen Bereiche heruntergeladen wurden.

  Zu diesem Zeitpunkt ist der Download abgeschlossen, und das Update kann jetzt installiert werden.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>Wie der Übermittlungsoptimierung für die Auslastung der Netzwerkbandbreite verringert

Delivery-Optimierung (DO) ist eine selbst organisierenden verteilter Cache-Lösung für Unternehmen, um die Auslastung der Netzwerkbandbreite für Updates des Betriebssystems, Upgrades beim Betriebssystem und Anwendungen zu reduzieren. Führen Sie ermöglicht Clients, die die Elemente aus anderen Quellen (z. B. andere Peers im Netzwerk) in Verbindung mit dem angegebenen Speicherort (dem ISV-Dateicache in diesem Szenario) herunterladen.

Standardmäßig in Windows 10 Enterprise und Education ermöglicht die Peer-zu-Peer-Freigabe, nur im Netzwerk des Unternehmens, jedoch können Sie dies mithilfe einer Gruppenrichtlinie oder die Einstellungen für mobile Geräte (MDM) auf unterschiedliche Weise konfigurieren.

Finden Sie unter [konfigurieren Delivery Optimization für Windows 10-updates](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization) für Weitere Informationen zu führen.
