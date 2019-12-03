---
title: ISV-Unterstützung für Express-Updatebereitstellung
description: 'WSUS-Thema (Windows Server Update Services): Konfigurieren der Express-Updatebereitstellung durch unabhängige Softwarehersteller (ISVs) per WSUS'
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
author: sakitong
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: a4880a1a66d9c722cfda9e194c4eff38c5058674
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361723"
---
# <a name="express-update-delivery-isv-support"></a>ISV-Unterstützung für Express-Updatebereitstellung

>Gilt für: Windows 10, Windows Server 2016

Windows 10-Updatedownloads können groß sein, da jedes Paket alle zuvor veröffentlichten Korrekturen enthält, um Konsistenz und Einfachheit sicherzustellen.  

Seit Version 7 konnte für Windows die Größe von Downloads mit Windows-Updates mit dem Feature [Express](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx#Anchor_2) reduziert werden. Dieses Feature wird von Verbrauchergeräten zwar standardmäßig unterstützt, aber für Windows 10 Enterprise-Geräte muss Windows Server Update Services (WSUS) verwendet werden, um Express nutzen zu können.

## <a name="how-microsoft-supports-express"></a>Unterstützung von Express durch Microsoft

- **Express für eigenständiges WSUS**

    Die Express-Updatebereitstellung ist [für alle unterstützten Versionen von WSUS bereits verfügbar](https://technet.microsoft.com/library/cc708456(v=ws.10).aspx).

- **Express auf Geräten, die direkt mit Windows Update verbunden sind** 

    Für Verbrauchergeräte wird der Express-Download unterstützt: Der Windows Update-Client (WU) wird zum Überprüfen, Herunterladen und Installieren von Updates verwendet. Während der Downloadphase fordert der WU-Client Express-Pakete an und lädt die entsprechenden Bytebereiche herunter.

-  **Enterprise-Geräte, die mit [Windows Update for Business](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)** verwaltet werden, profitieren ebenfalls von der Unterstützung der Express-Updatebereitstellung ohne Änderung der Konfiguration.

## <a name="how-isvs-can-take-advantage-of-express"></a>Nutzen von Express durch ISVs

ISVs können WSUS und den WU-Client verwenden, um die Express-Updatebereitstellung zu unterstützen. Microsoft empfiehlt die folgenden drei Schritte, die in den folgenden Abschnitten ausführlicher erläutert werden:

1.  [**Konfigurieren von WSUS**](#BKMK_1)

    WSUS-Server ist für Überprüfungs- und Updatesynchronisierungen erforderlich (weitere Informationen [hier](https://technet.microsoft.com/library/dn800972(v=ws.11).aspx))

2.  [**Angeben und Füllen eines ISV-Dateicaches**](#BKMK_2)

    Die Verwendung eines ISV-Dateicaches wird empfohlen, um den Updateinhalt zu hosten, also die CABINET-Dateien(.cab) des Updates und die Express-Pakete (.psf).

3.  [**Einrichten eines ISV-Client-Agents zum Steuern von WU-Clientvorgängen**](#BKMK_3)

>[!NOTE]
>Das kumulative Update für Windows 10 Version 1607 vom Januar 2017 ([KB3213986 (Betriebssystembuild 14393.693)](https://support.microsoft.com/en-us/help/4009938/january-10-2017-kb3213986-os-build-14393-693)) muss installiert sein.
    
   - Mit dem ISV-Client-Agent wird festgelegt, welche Updates genehmigt und wann Updates heruntergeladen und installiert werden.
   - Mit dem WU-Client werden die herunterzuladenden Bytebereiche ermittelt, und die Downloadanforderung wird initiiert.

### <a name="BKMK_1"></a>Schritt 1: Konfigurieren von WSUS

WSUS dient als Schnittstelle für Windows Update und zum Verwalten aller Metadaten zur Beschreibung von Express-Paketen, die heruntergeladen werden müssen. Informationen zur Bereitstellung findest du unter [**Übersicht über Windows Server Update Services 3.0 SP2**](https://technet.microsoft.com/library/dd939931(v=ws.10).aspx). Nachdem WSUS bereitgestellt wurde, musst du zunächst die Entscheidung treffen, ob Updateinhalte lokal auf dem WSUS-Server gespeichert werden sollen. Beim Konfigurieren von WSUS empfehlen wir, Updates nicht lokal zu speichern. Hierbei wird angenommen, dass du bereits über Software verfügst, mit der die Bereitstellung dieser Pakete in deiner Umgebung gesteuert wird. Weitere Informationen zur Konfiguration des lokalen WSUS-Speichers findest du unter [**Festlegen des Speicherorts für Updates**](https://technet.microsoft.com/library/cc720494(v=ws.10).aspx).

### <a name="BKMK_2"></a>Schritt 2: Angeben und Füllen des ISV-Dateicaches 

#### <a name="specify-the-isv-file-cache"></a>Angeben des ISV-Dateicaches

Mit neuen clientseitigen Einstellungen für die Gruppenrichtlinie und die Verwaltung mobiler Geräte (Mobile Device Management, MDM), die in der [**Referenz zum Konfigurationsdienstanbieter**](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) ausführlich beschrieben sind, wird der Speicherort des ISV-Dateicaches beschrieben.

| **Name**                                              | **Beschreibung**                                                                                                                                                      |
|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Konfiguriere einen anderen Downloadspeicherort für Updates. | Gibt einen alternativen Intranetserver zum Hosten von Updates von Microsoft Update an. Du kannst diesen Updatedienst dann verwenden, um Computer in deinem Netzwerk automatisch zu aktualisieren. |

Beim Einrichten des alternativen Downloadspeicherorts für den ISV-Dateicache hast du zwei Optionen:

1. **Gib einen ISV-HTTP-Serverhostnamen an**. Dies ist der ISV-Dateicache.
    
    Bei diesem Ansatz wird der WU-Client so konfiguriert, dass Downloadanforderungen an den HTTP-Server gesendet werden, der in der Richtlinie angegeben ist.

2. **Angeben von „localhost“**
 
    Bei diesem Ansatz wird der WU-Client so konfiguriert, dass Downloadanforderungen an „localhost“ gesendet werden. Der ISV-Client-Agent kann diese Anforderungen dann verarbeiten und entsprechend weiterleiten, um die Downloadanforderung zu erfüllen.

> [!IMPORTANT]
> Für den ISV-Dateicache ist Folgendes erforderlich:                                                          
> - Der Server muss HTTP 1.1-konform gemäß RFC sein: <http://www.w3.org/Protocols/rfc2616/rfc2616.html>                                                                                                                                                                
> Der Webserver muss [**HEAD**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)- und [**GET**](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.htm)-Anforderungen unterstützen.<br>                                                                                                                                                                                                                                                                                                  - Teilbereichsanforderungen<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   - Keep-Alive<br>                                                                                                                                                                                                                                                                                                                                                                                                                            - „Transfer-Encoding:chunked“ nicht verwenden                                                                                                 

#### <a name="populate-the-isv-file-cache"></a>Füllen des ISV-Dateicaches

Der ISV-Dateicache muss mit Dateien gefüllt werden, die den auf verwalteten Clients zu installierenden Updates zugeordnet sind. 

**Fülle den ISV-Dateicache wie folgt auf:**

1. Verwende [WSUS-APIs](https://msdn.microsoft.com/library/windows/desktop/microsoft.updateservices.administration.updatefile(v=vs.85).aspx), um auf den Dateipfad des Updates und den Dateinamen für den MU-Dienst zuzugreifen.

    Die Metadaten für jedes Update auf dem WSUS-Server enthalten den Dateipfad des Updates und den Dateinamen unter Microsoft Update wie folgt (Microsoft Update-Hostname in Fettdruck, gefolgt von Dateipfad und -name): **<http://download.windowsupdate.com>** /c/msdownload/update/software/updt/2016/09/windows10.0-kb3195781-x64_0c06079bccc35cba35a48bd2b1ec46f818bd2e74.msu

2. Lade Dateien von Microsoft Update herunter, und speichere sie mit einem dieser beiden Verfahren im ISV-Dateicache: 

   - Speichern der Dateien, indem du **den gleichen Ordnerpfad wie für den MU-Dienst** verwendest

   - Speichern der Dateien mit einem **vom ISV definierten Ordnerpfad**

     Der HTTP-Server (bzw. „localhost“) sollte so eingerichtet werden, dass **HTTP GET**-Anforderungen, in denen auf den MU-Ordnerpfad und den zugehörigen Dateinamen verwiesen wird, an den Speicherort der ISV-Datei umgeleitet werden.

### <a name="BKMK_3"></a>Schritt 3: Einrichten eines ISV-Client-Agents zum Steuern von WU-Clientvorgängen

Der ISV-Client-Agent orchestriert den Download und die Installation von genehmigten Updates, indem der folgende Workflow verwendet wird:

1.  Der ISV-Client-Agent ruft den WU-Client auf, um einen Überprüfungsvorgang für den WSUS-Server auszuführen.

2.  Beim Überprüfungsvorgang werden die jeweiligen Updates für den WU-Client zurückgegeben.

3.  Der ISV-Client bestimmt, welche Updates genehmigt, heruntergeladen und installiert werden.

4.  Der ISV-Client-Agent ruft den WU-Client auf, um die genehmigten Updates herunterzuladen.

5.  Nachdem die Updates heruntergeladen wurden, ruft der ISV-Client-Agent den WU-Client auf, um die genehmigten Updates zu installieren.

Weitere Informationen zur Nutzung des WU-Clients zum Überprüfen, Herunterladen und Installieren von Updates findest du unter [Suchen, Herunterladen und Installieren von Updates](https://msdn.microsoft.com/library/windows/desktop/aa387102(v=vs.85).aspx).

### <a name="download-workflow-options"></a>Optionen des Workflows für den Download

Hier sind zwei Abbildungen mit den Optionen des Workflows für den Download eines ISV-Dateicaches angegeben:

![Workflow 1](../../media/express-update-delivery-isv-support/image1.png)

![Workflow 2](../../media/express-update-delivery-isv-support/image2.png)
### <a name="how-express-download-works"></a>Funktionsweise des Express-Downloads

- Für Betriebssystemupdates, die Express unterstützen, sind zwei Versionen der Dateinutzlast im Dienst gespeichert:

  - **Vollständige Dateiversion**: Ersetzt im Wesentlichen die lokalen Versionen der Updatebinärdateien.

  - **Express-Version**: Enthält die Deltas, die zum Patchen der vorhandenen Binärdateien auf dem Gerät erforderlich sind. 

    Sowohl auf die vollständige Dateiversion als auch auf die Express-Version wird in den Metadaten des Updates verwiesen, die im Rahmen der Überprüfungsphase auf den Client heruntergeladen wurden. 

    **Der Express-Download funktioniert wie folgt:**

    Der WU-Client versucht zuerst, Express herunterzuladen. Unter bestimmten Umständen wird bei Bedarf auf die vollständige Dateiversion zurückgegriffen (z. B. bei Verwendung eines Proxys, der Bytebereichsanforderungen nicht unterstützt).

  1. Wenn der WU-Client einen Express-Download initiiert, **lädt der WU-Client zuerst einen Stub herunter**, der Teil des Express-Pakets ist.

  2. **Der WU-Client sendet diesen Stub an Windows Installer**, der den Stub für eine lokale Inventur verwendet. Hierbei werden die Deltas der Datei auf dem Gerät damit verglichen, was erforderlich ist, um die neueste Version der bereitgestellten Datei abzurufen.

  3. **Windows Installer fordert dann den WU-Client zum Herunterladen der Bereiche auf**, die als erforderlich bestimmt wurden.

  4. **Der WU-Client lädt diese Bereiche herunter und leitet sie an Windows Installer weiter**, der die Bereiche anwendet und dann bestimmt, ob weitere Bereiche erforderlich sind. Dies wird wiederholt, bis Windows Installer den WU-Client informiert, dass alle erforderlichen Bereiche heruntergeladen wurden.

  Der Download ist dann abgeschlossen, und das Update kann installiert werden.

### <a name="how-delivery-optimization-reduces-bandwidth-consumption"></a>Reduzierung der Bandbreitennutzung durch Übermittlungsoptimierung

Die Übermittlungsoptimierung ist eine selbstorganisierende Lösung für verteilten Cache für Unternehmen, die die Bandbreitennutzung für Updates bzw. Upgrades von Betriebssystemen und Anwendungen reduzieren möchten. Dank der Übermittlungsoptimierung können Clients diese Elemente basierend auf dem angegebenen Downloadspeicherort (in diesem Fall der ISV-Dateicache) von alternativen Quellen (z. B. andere Peers im Netzwerk) herunterladen.

Standardmäßig ermöglicht die Übermittlungsoptimierung in Windows 10 Enterprise und Education die Peer-to-Peer-Freigabe nur innerhalb des Netzwerks der Organisation. Du kannst dies über die Gruppenrichtlinie und in den Einstellungen der Verwaltung mobiler Geräte (Mobile Device Management, MDM) aber abweichend konfigurieren.

Weitere Informationen zur Übermittlungsoptimierung findest du unter [Übermittlungsoptimierung für Windows 10-Updates](https://technet.microsoft.com/itpro/windows/manage/waas-delivery-optimization).
