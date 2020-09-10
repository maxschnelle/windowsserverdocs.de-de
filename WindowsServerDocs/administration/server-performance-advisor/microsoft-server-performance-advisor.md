---
title: Microsoft Server Performance Advisor
description: Microsoft Server Performance Advisor
ms.assetid: 468ebcb3-9eaf-477c-ab10-e3f1b3ce63dc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.topic: article
ms.openlocfilehash: bd359e71cfb48ecd8aab24a8538369622dd1d271
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627700"
---
# <a name="microsoft-server-performance-advisor"></a>Microsoft Server Performance Advisor

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Laden Sie Microsoft Server Performance Advisor (Spa) herunter, um bei der Bereitstellung von Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 Leistungsprobleme zu diagnostizieren. Spa generiert umfassende Diagnose Berichte und-Diagramme und bietet Empfehlungen, mit deren Hilfe Sie Probleme schnell analysieren und Korrekturmaßnahmen entwickeln können.

-   [Übersicht über den Server Performance Advisor](#bkmk-aboutspa)

-   [Herunterladen von Server Performance Advisor](#bkmk-downloadspa)

-   [Server Performance Advisor-Benutzerhandbuch](server-performance-advisor-users-guide.md)

-   [Server Performance Advisor Pack-Entwicklungsleitfaden](server-performance-advisor-pack-development-guide.md)

## <a name="overview-of-server-performance-advisor"></a><a href="" id="bkmk-aboutspa"></a>Übersicht über den Server Performance Advisor

Der Server Performance Advisor besteht aus zwei Teilen: dem Spa-Framework und den Spa Advisor-Paketen.

### <a name="the-server-performance-advisor-framework"></a>Das Server Performance Advisor-Framework

Die Engine, die für das Erfassen von Daten verantwortlich ist, die von den Advisor-Paketen festgelegt werden, das Schreiben der gesammelten Daten in eine Microsoft SQL Server Datenbank, das Erstellen einer IT-freundlichen Umgebung zum Ausführen von Skripts für die Spa Advisor-Pakete und das Anzeigen der abschließenden Berichte. Sie müssen das Spa-Framework nur in der Spa-Konsole installieren. Die Spa-Konsole kann entweder auf einem eigenständigen Computer installiert werden, um Remote auf die zu testenden Server zuzugreifen oder auf einem getesteten Server installiert zu werden.

### <a name="server-performance-advisor-packs"></a>Server Performance Advisor Packs

Spa Advisor Packs stellen den Mittelpunkt aller Optimierungs Regeln dar, die aus einer Reihe von Metadaten und SQL-Skriptdateien bestehen. Spa umfasst die folgenden Advisor-Pakete:

-   Das Core-Betriebssystem Advisor-Paket analysiert die Leistung allgemeiner Betriebssystemfunktionen unabhängig von spezialisierten Server Rollen.

-   Das Internet Information Server (IIS) Advisor Pack verfolgt die Leistung von IIS.

-   Mit dem Hyper-v Advisor Pack wird die allgemeine Leistung der Hyper-v-Server Rolle analysiert.

    **Hinweis** Das Hyper-V Advisor Pack analysiert keine Gast Betriebssysteme.



-   Das Active Directory Advisor Pack analysiert die allgemeine Leistung der Active Directory-Rolle.

Spa bietet auch ein erweiterbares Modell für Entwickler, die nicht von Microsoft unterstützt werden, um Advisor Packs entsprechend Ihren Anforderungen zu schreiben.

**Hinweis** Spa kann nicht alle Hardware-und Benutzer szenariokontexte verstehen. Verwenden Sie die Empfehlungen, die vom Tool bereitgestellt werden, um Entscheidungen zu treffen und die Konsequenzen von möglichen Änderungen zu verstehen, die an den Servern vorgenommen werden.



## <a name="download-server-performance-advisor"></a><a href="" id="bkmk-downloadspa"></a>Herunterladen von Server Performance Advisor


Verwenden Sie die folgenden Links zum Herunterladen von Server Performance Advisor für Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008:

-   [Microsoft Server Performance Advisor 3,1 (32 Bit)](https://go.microsoft.com/fwlink/p/?linkid=327751)

-   [Microsoft Server Performance Advisor 3,1 (64 Bit)](https://go.microsoft.com/fwlink/p/?linkid=327752)

Sie können die Dateien in der CAB-Datei mit den folgenden Befehlen extrahieren:

-   für die x86-Version: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_x86.cab`

-   für die x64-Version: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_amd64.cab`

**Vorsicht** Wenn Sie die CAB-Datei extrahieren, muss Spa die hierarchische Verzeichnisstruktur beibehalten, damit Sie ordnungsgemäß funktioniert. Abhängig von den CAB-Tools, die auf dem Server installiert sind, kann die Extraktion zu einer nicht operativen Verzeichnisstruktur führen. Um die hierarchische Verzeichnisstruktur beizubehalten, können Sie ein Tool zum Extrahieren von Hilfsprogramm verwenden, das eine Datei Verzeichnisstruktur extrahiert.

Wenn das CAB-Extraktions Tool die Dateien ordnungsgemäß extrahiert hat, werden die Unterordner automatisch im Extraktions Zielordner angezeigt.

### <a name="spa-prerequisites"></a>Voraussetzungen für Spa

Die Spa-Konsole erfordert, dass die folgende Software installiert ist:

-   Microsoft .NET Framework 4

-   SQL Server 2008 R2 Express SP1 oder Microsoft SQL Server 2008 R2 SP1

Neuere Versionen sind möglicherweise kompatibel. Alle bekannten Produkt Inkompatibilitäten mit der Spa-Konsole werden vermerkt.
