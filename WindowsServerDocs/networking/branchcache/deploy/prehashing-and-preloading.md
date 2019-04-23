---
title: Prehashing und Vorabladen von Inhalt auf gehostete Cacheserver (optional)
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b421132a44240520e3e3ba294623584c36b18ab4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867001"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Prehashing und Vorabladen von Inhalt auf gehostete Cacheserver (optional)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um die Erstellung von Inhaltsinformationen – so genannte Hashes - auf BranchCache-fähigen Web- und Dateiservern zu erzwingen. Sie können auch auf Datei-und Web in Pakete Datenerfassung, die für remote gehosteten Cacheserver übertragen werden können.  Dadurch erhalten Sie mit der Möglichkeit, Inhalte auf remote gehosteten Cacheservern vorab zu laden, damit Daten für den ersten Clientzugriff verfügbar ist.  
  
Sie müssen ein Mitglied sein **Administratoren**, oder führen Sie dieses Verfahren entspricht.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>Unterziehen Inhalt und den Inhalt auf gehosteten Cacheservern vorab zu laden  
  
1.  Melden Sie sich auf die Datei oder einen Webserver, der die Daten enthält, die Sie vorab geladen werden soll, und identifizieren Sie die Ordner und Dateien, die Sie auf eine oder mehrere remote gehosteten Cacheserver laden möchten.  
  
2.  Führen Sie Windows PowerShell als Administrator an. Für jeden Ordner und Dateien, führen Sie entweder die `Publish-BCFileContent` Befehl oder die `Publish-BCWebContent` Befehl hängt vom Inhaltsserver, hasherzeugung auslösen und zum Hinzufügen von Daten zu einem Datenpaket.  
  
3.  Nachdem alle Daten wurde für das Datenpaket hinzugefügt, exportieren Sie es mithilfe der `Export-BCCachePackage` Befehl aus, um eine Datendatei für das Paket zu erstellen.  
  
4.  Verschieben Sie die Paket-Datendatei zu remote gehosteten Cacheserver, indem Sie die Wahl der Technologie für die Übertragung von Dateien.  FTP-"," SMB "," HTTP "," DVD "und" tragbaren Festplatten sind alle geeignete Transporte.  
  
5.  Importieren Sie die Paketdatei der Daten auf remote gehosteten Cacheserver mithilfe der `Import-BCCachePackage` Befehl.  
  

