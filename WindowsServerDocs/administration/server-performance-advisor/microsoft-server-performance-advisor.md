---
title: Microsoft Server Performance Advisor
description: Microsoft Server Performance Advisor
ms.assetid: 468ebcb3-9eaf-477c-ab10-e3f1b3ce63dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: manage
ms.openlocfilehash: ab124f3efabf2ac3ae8904157a81587c0c21ebb5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856331"
---
# <a name="microsoft-server-performance-advisor"></a>Microsoft Server Performance Advisor

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Herunterladen von Microsoft Server Performance Advisor (SPA) zum Diagnostizieren von Leistungsproblemen in einem Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008-Bereitstellung. SPA generiert umfassende diagnostische Berichte und Diagramme sowie Empfehlungen unterstützen Sie beim schnellen Analysieren von Problemen und korrekturmaßnahmen zu entwickeln.

-   [Übersicht über die Server Performance Advisor](#bkmk-aboutspa)

-   [Server Performance Advisor herunterladen](#bkmk-downloadspa)

-   [Server Performance Advisor-Benutzerhandbuch](server-performance-advisor-users-guide.md)

-   [Server Performance Advisor Pack-Entwicklerhandbuch](server-performance-advisor-pack-development-guide.md)

## <a href="" id="bkmk-aboutspa"></a>Übersicht über die Server Performance Advisor

Server Performance Advisor besteht aus zwei Teilen, die SPA-Framework und die SPA-Advisor-Packs.

### <a name="the-server-performance-advisor-framework"></a>Der Server Performance Advisor-framework

Die Engine, die für das Sammeln von Daten, die von den Advisor-Packs festgelegt ist, schreiben die gesammelten Daten in einer Microsoft SQL Server-Datenbank, Erstellen einer IT-freundlichen Umgebung zum Ausführen von Skripts für die Advisor-Packs SPA und zeigt die endgültige Berichte verantwortlich ist. Sie müssen nur die SPA-Framework in der SPA-Konsole zu installieren. Die SPA-Konsole kann entweder auf einem eigenständigen Computer Remote Zugriff auf den zu testenden Server oder auf einem Server unter Test installiert werden, installiert werden.

### <a name="server-performance-advisor-packs"></a>Server Performance Advisor Packs

Advisor-Packs SPA spielen für alle Regeln, Optimierung, die aus einer Reihe von Metadaten und SQL-Skriptdateien bestehen. SPA umfasst die folgenden Packs für Advisor:

-   Das Core-Betriebssystem Advisor Pack analysiert die Leistung der allgemeinen Betriebssystemfunktionen, unabhängig von der speziellen-Serverrollen an.

-   Das Internet Information Server (IIS)-Advisor-Pack verfolgt die Leistung von IIS.

-   Das Hyper-V-Advisor-Pack analysiert die allgemeine Leistung der Hyper-V-Serverrolle.

    **Beachten Sie** Gastbetriebssysteme werden von Advisor-Pack für die Hyper-V nicht analysiert.

     

-   Das active Directory-Pack Advisor analysiert die allgemeine Leistung von active Directory-Rolle.

SPA bietet auch ein erweiterbares Modell für nicht-Microsoft-Entwickler zum Schreiben von Advisor-Packs ihren Anforderungen entsprechend.

**Beachten Sie** SPA nicht alle Hardware- und Benutzer-Szenario-Kontexte nicht verstehen. Verwenden Sie die Empfehlungen, die bereitgestellt werden, von dem Tool können Sie die Entscheidungen treffen und die Auswirkungen von potenziellen Änderungen, die mit den Servern vorgenommen werden.

 

## <a href="" id="bkmk-downloadspa"></a>Server Performance Advisor herunterladen


Verwenden Sie die folgenden Links, um Server Performance Advisor für Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 herunterzuladen:

-   [Microsoft Server Performance Advisor 3.1 (32-Bit)](https://go.microsoft.com/fwlink/p/?linkid=327751)

-   [Microsoft Server Performance Advisor 3.1 (64-Bit)](https://go.microsoft.com/fwlink/p/?linkid=327752)

Sie können die Dateien in die CAB-Datei extrahieren, mithilfe der folgenden Befehle:

-   für die X86 Version: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_x86.cab`

-   für die X64 Version: `extrac32.exe /e /a /l  d:\SPA   d:\SPA\SPAPlus\_amd64.cab`

**Vorsicht** SPA muss, wenn Sie die CAB-Datei extrahiert haben, erhalten die hierarchische Verzeichnisstruktur, um korrekt zu funktionieren. Abhängig von den CAB-Tools, die auf dem Server installiert sind, kann die Extrahierung in einer nicht betriebsbereit Verzeichnisstruktur führen. Wenn Sie die hierarchische Verzeichnisstruktur beibehalten möchten, können Sie eine CAB-Datei extrahieren Utility-Tool, das eine Verzeichnisstruktur für die Datei extrahiert.

Wenn das Tool zur skriptressourcenextraktion CAB-Datei ordnungsgemäß die Dateien extrahiert haben, werden die Unterordner automatisch in den Zielordner für die Extraktion angezeigt.

### <a name="spa-prerequisites"></a>SPA-Voraussetzungen

Der SPA-Konsole erfordert, dass die folgende Software installiert ist:

-   Microsoft .NET Framework 4

-   SQL Server 2008 R2 Express SP1 oder Microsoft SQL Server 2008 R2 SP1

Neuere Versionen können kompatibel sein. Bekannte Inkompatibilitäten mit SPA-Konsole werden gekennzeichnet.
