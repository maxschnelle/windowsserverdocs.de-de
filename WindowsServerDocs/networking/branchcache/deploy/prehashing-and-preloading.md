---
title: Prehashing und Vorabladen von Inhalt auf gehosteten Cacheserver (Optional)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das veranschaulicht, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 45adc982b7ced1a6cc40f978feee81202f822b0c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937529"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Prehashing und Vorabladen von Inhalt auf gehosteten Cacheserver (Optional)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie die Erstellung von Inhaltsinformationen, auch als Hashes bezeichnet, auf BranchCache-aktivierten Web-und Dateiservern erzwingen. Sie können auch die Daten auf Datei-und Webservern in Paketen zusammenfassen, die auf Remote gehostete Cache Server übertragen werden können.  Dadurch haben Sie die Möglichkeit, Inhalte auf Remote gehosteten Cache Servern vorab zu laden, damit die Daten für den ersten Client Zugriff verfügbar sind.

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>So versehen Sie Inhalt vorab und laden den Inhalt auf gehosteten Cache Servern vorab

1.  Melden Sie sich bei der Datei oder dem Webserver an, die die Daten enthält, die Sie vorab laden möchten, und identifizieren Sie die Ordner und Dateien, die Sie auf einem oder mehreren Remote gehosteten Cache Servern laden möchten.

2.  Führen Sie Windows PowerShell als Administrator aus. Führen Sie für jeden Ordner und jede Datei entweder den `Publish-BCFileContent` Befehl oder den Befehl aus. Dies hängt `Publish-BCWebContent` vom Typ des Inhalts Servers ab, um die Hash Generierung zu initiieren und Daten einem Datenpaket hinzuzufügen.

3.  Nachdem alle Daten dem Datenpaket hinzugefügt wurden, exportieren Sie Sie, indem Sie den `Export-BCCachePackage` Befehl verwenden, um eine Datenpaket Datei zu entwickeln.

4.  Verschieben Sie die Datenpaket Datei auf die Remote gehosteten Cache Server, indem Sie die Datei Übertragungstechnologie auswählen.  FTP, SMB, http, DVD und Portable Festplatten sind alle funktionierenden Transporte.

5.  Importieren Sie die Datenpaket Datei auf den Remote gehosteten Cache Servern, indem Sie den `Import-BCCachePackage` Befehl verwenden.


