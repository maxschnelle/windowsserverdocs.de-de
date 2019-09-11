---
title: ISV-Unterstützung für Express-Updatebereitstellung
description: 'Windows Server Update Service (WSUS)-Thema: wie unabhängige Software Anbieter (ISV) die Express-Update Bereitstellung mithilfe von WSUS konfigurieren können'
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
ms.openlocfilehash: 0f5893d47219e9263ed7f35bee472848a47c6164
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868736"
---
# <a name="express-update-delivery-isv-support"></a>ISV-Unterstützung für Express-Updatebereitstellung

>Gilt für: Windows 10, Windows Server 2016

Downloads für Windows 10-Updates können sehr umfangreich sein, da jedes Paket alle zuvor veröffentlichten Korrekturen enthält, um die Konsistenz und Einfachheit sicherzustellen.  

Seit Version 7 konnte Windows die Größe der Windows Update Downloads mit einer Funktion namens " [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2)" reduzieren, und auch wenn consumergeräte diese standardmäßig unterstützen, erfordern Windows 10 Enterprise-Geräte Windows Server Update Services (WSUS). Vorteil von Express.

## <a name="how-microsoft-supports-express"></a>Wie Microsoft Express unterstützt

- **Express auf WSUS Standalone**

    Die Express-Update Bereitstellung ist bereits [für alle unterstützten Versionen von WSUS verfügbar](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx).

- **Express auf Geräten, die direkt mit Windows Update verbunden sind** 

    Consumergeräte unterstützen den Express-Download: Sie verwenden den Windows Update (Wu)-Client, um Updates zu scannen, herunterzuladen und zu installieren. Während der Download Phase fordert der Wu-Client Express-Pakete an und lädt die entsprechenden Byte Bereiche herunter.

-  **Enterprise-Geräte, die mit [Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** verwendet werden, profitieren ebenfalls von der Unterstützung der Express-Updatebereitstellung ohne Änderung der Konfiguration.

## <a name="how-isvs-can-take-advantage-of-express"></a>Wie ISVs Express nutzen können

ISVs können WSUS und den Wu-Client verwenden, um die Express-Update Bereitstellung zu unterstützen. Microsoft empfiehlt die folgenden drei Schritte, die in den folgenden Abschnitten ausführlich erläutert werden:

1.  [**Konfigurieren von WSUS**](#BKMK_1)

    Der WSUS-Server ist für die Überprüfung & Aktualisierungs Synchronisierung erforderlich (Weitere Informationen finden Sie [hier](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx)).

2.  [**Einen ISV-Dateicache angeben und Auffüllen**](#BKMK_2)

    Ein ISV-Dateicache wird empfohlen, um den Update Inhalt zu hosten. dazu gehören die Update CAB-Dateien (CAB-Dateien) und die Express-Pakete (PSF-Dateien).

3.  [**Einrichten eines ISV-Client-Agents zum Weiterleiten von Wu-Client Vorgängen**](#BKMK_3)

>[!NOTE]
>Erfordert die Installation des kumulativen Updates für Windows 10, Version 1607, in (oder höher) Januar 2017 ([KB3213986 (OS Build 14393,693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693) .
    
   - Der ISV-Client-Agent bestimmt, welche Updates genehmigt werden sollen und wann Updates heruntergeladen und installiert werden.
   - Der Wu-Client bestimmt die herunter zuladbare Byte Bereiche und initiiert die Download Anforderung.

### <a name="BKMK_1"></a>Schritt 1: Konfigurieren von WSUS

WSUS fungiert als Schnittstelle, um alle Metadaten zu Windows Update und zu verwalten, die Express-Pakete beschreiben, die heruntergeladen werden müssen. Wenn Sie bereitstellen müssen, finden Sie unter [**Übersicht über Windows Server Update Services 3,0 SP2**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx)Weitere Informationen. Nach der Bereitstellung von WSUS besteht der primäre Aspekt darin, ob Update Inhalte lokal auf dem WSUS-Server gespeichert werden sollen. Beim Konfigurieren von WSUS wird empfohlen, Updates nicht lokal zu speichern. Dabei wird davon ausgegangen, dass Sie bereits über Software verfügen, die die Bereitstellung dieser Pakete in Ihrer Umgebung leitet. Weitere Informationen zum Konfigurieren des lokalen WSUS-Speichers finden Sie unter Bestimmen des Speicher Orts [**für Updates**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx).

### <a name="BKMK_2"></a>Schritt 2: Geben Sie den ISV-Datei Cache an und füllen ihn aus. 

#### <a name="specify-the-isv-file-cache"></a>Geben Sie den ISV-Datei Cache an.

Die neuen Einstellungen für die Client seitige Gruppenrichtlinie und die Verwaltung mobiler Geräte (Mobile Device Management, MDM), die in der [**Referenz zum Konfigurations Dienstanbieter**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) beschrieben werden

| **Name**                                              | **Beschreibung**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Konfigurieren Sie einen alternativen Download Speicherort für Updates. | Gibt einen alternativen Intranetserver zum Hosten von Updates aus Microsoft Update an. Anschließend können Sie mit diesem Aktualisierungs Dienstcomputer im Netzwerk automatisch aktualisieren. |

Beim Einrichten des alternativen Download Speicher Orts für den ISV-Dateicache gibt es zwei Optionen:

1. **Geben Sie einen ISV-http-Server Hostnamen an**, der der ISV-Dateicache ist.
    
    Bei diesem Ansatz wird der Wu-Client so konfiguriert, dass Download Anforderungen an den in der Richtlinie angegebenen HTTP-Server gestellt werden.

2. **Localhost angeben**
 
    Bei diesem Ansatz wird der Wu-Client so konfiguriert, dass Download Anforderungen an "localhost" gestellt werden. Dies ermöglicht es dem ISV-Client-Agent, diese Anforderungen und Routen nach Bedarf zu verarbeiten, um die Download Anforderung zu erfüllen.

> [!IMPORTANT]
> Der ISV-Dateicache erfordert Folgendes:                                                          
> - Der Server muss gemäß der RFC HTTP 1,1-kompatibel sein:<http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> Insbesondere muss der Webserver Unterstützung für                                                                                                                                                                                                                                       [**Head**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) -und [**Get**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm) -Anforderungen<br>                                                                                                                                                                                                                                                                                                  -Partielle Bereichs Anforderungen<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   -Keep-Alive<br>                                                                                                                                                                                                                                                                                                                                                                                                                            -Verwenden Sie "Transfer-Encoding: chunked" nicht.                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>Auffüllen des ISV-Datei Caches

Der ISV-Dateicache muss mit Dateien aufgefüllt werden, die mit den auf verwalteten Clients zu installierenden Updates verknüpft sind. 

**So füllen Sie den ISV-Dateicache auf:**

1. Verwenden Sie [WSUS-APIs](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx) , um auf den Dateipfad und den Dateinamen des Updates für den mu-Dienst zuzugreifen.

    Die Metadaten für jedes Update auf dem WSUS-Server enthalten den Dateipfad und den Dateinamen des Updates auf Microsoft Update wie folgt (Microsoft Update Hostname Fett, gefolgt von Dateipfad **<http://download.windowsupdate.com>** und Dateiname):/c/msdownload/Update/Software/updt/2016/09/ Windows 10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74. msu

2. Laden Sie Dateien aus Microsoft Update herunter, und speichern Sie Sie im ISV-Dateicache mithilfe einer dieser beiden Methoden: 

   - Speichern von Dateien mit **demselben Ordner Pfad wie auf dem mu-Dienst**

   - Speichern von Dateien mithilfe eines **ISV-definierten Ordner Pfads**

     Http-Server (oder localhost) leiten **HTTP Get** -Anforderungen, die auf den mu-Ordner Pfad und den Dateinamen verweisen, an den Speicherort der ISV-Datei weiter.

### <a name="BKMK_3"></a>Schritt 3: Einrichten eines ISV-Client-Agents zum Weiterleiten von Wu-Client Vorgängen

Der ISV-Client-Agent orchestriert den Download und die Installation genehmigter Updates mithilfe des folgenden empfohlenen Workflows:

1.  Der ISV-Client-Agent ruft den Wu-Client auf, um den WSUS-Server zu scannen.

2.  Bei der Überprüfung wird der Satz der anwendbaren Updates für den Wu-Client zurückgegeben.

3.  Der ISV-Client bestimmt, welche Updates genehmigt, heruntergeladen und installiert werden.

4.  Der ISV-Client-Agent ruft den Wu-Client zum Herunterladen der genehmigten Updates auf

5.  Nachdem die Updates heruntergeladen wurden, ruft der ISV-Client-Agent den Wu-Client auf, um die genehmigten Updates zu installieren.

Weitere Informationen zum Überprüfen, herunterladen und Installieren von Updates finden Sie unter [suchen, herunterladen](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx) und Installieren von Updates.

### <a name="download-workflow-options"></a>Workflow Optionen herunterladen

Im folgenden sind zwei Abbildungen der Download Workflow Optionen aus einem ISV-Dateicache aufgeführt:

![Workflow 1](../../media/express-update-delivery-isv-support/image1.png)

![Workflow 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Wie der Express-Download funktioniert

- Für Betriebssystemupdates, die Express unterstützen, sind zwei Versionen der Dateinutzlast im Dienst gespeichert:

  - **Vollständige Dateiversion** : im Grunde ersetzen Sie die lokalen Versionen der Update Binärdateien.

  - **Express Version** : enthält die Delta Dateien, die zum Patchen der vorhandenen Binärdateien auf dem Gerät erforderlich sind. 

    In den Metadaten des Updates wird auf die vollständige Dateiversion und die Express-Version verwiesen, die im Rahmen der Überprüfungsphase auf den Client heruntergeladen wurde. 

    **Der Express-Download funktioniert wie folgt:**

    Der Wu-Client versucht, Express zuerst herunterzuladen, und kann bei Bedarf in bestimmten Situationen auf die vollständige Datei zurückgreifen (z. b. Wenn ein Proxy durchlaufen wird, der keine Byte Bereichs Anforderungen unterstützt).

  1. Wenn der Wu-Client einen Express-Download initiiert, **lädt der Wu-Client zuerst einen Stub**herunter, der Teil des Express-Pakets ist.

  2. **Der Wu-Client übergibt diesen Stub an den Windows Installer**, der den Stub zum Durchführen eines lokalen Inventars verwendet. dabei werden die Deltas der Datei auf dem Gerät mit dem verglichen, was erforderlich ist, um die neueste Version der bereitgestellten Datei zu erhalten.

  3. Der **Windows Installer fordert dann den Wu-Client an, die Bereiche herunterzuladen** , die als erforderlich eingestuft wurden.

  4. **Der Wu-Client lädt diese Bereiche herunter und übergibt sie an den Windows Installer**, der die Bereiche anwendet und dann bestimmt, ob zusätzliche Bereiche benötigt werden. Dies wird wiederholt, bis der Wu-Client vom Windows Installer darüber informiert wird, dass alle erforderlichen Bereiche heruntergeladen wurden.

  Zu diesem Zeitpunkt ist der Download abgeschlossen, und das Update kann jetzt installiert werden.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>Verringern der Bandbreitennutzung durch Übermittlungs Optimierung

Die Übermittlungs Optimierung (Do) ist eine selbst organisierende Lösung für verteilte Caches für Unternehmen, die die Bandbreitennutzung für Betriebssystemupdates, Betriebssystem Upgrades und Anwendungen reduzieren möchten. Ermöglicht Clients das Herunterladen dieser Elemente aus alternativen Quellen (z. b. anderen Peers im Netzwerk) in Verbindung mit dem angegebenen Download Speicherort (der ISV-Dateicache in diesem Szenario).

In Windows 10 Enterprise und Education ermöglicht die Peer-zu-Peer-Freigabe standardmäßig nur im eigenen Netzwerk der Organisation, Sie können Sie jedoch unterschiedlich konfigurieren, indem Sie Gruppenrichtlinie und MDM-Einstellungen (Mobile Device Management, Verwaltung mobiler Geräte) verwenden.

Weitere Informationen zu do finden Sie unter Konfigurieren der Übermittlungs [Optimierung für Windows 10-Updates](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization) .
