---
title: Prehashing und Vorabladen von Inhalt auf gehostete Cacheserver (optional)
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das veranschaulicht, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 5a09d9f1-1049-447f-a9bf-74adf779af27
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1a0694ebe30c5a927fb2f1152adc792f8b0c9157
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356390"
---
# <a name="prehashing-and-preloading-content-on-hosted-cache-servers-optional"></a>Prehashing und Vorabladen von Inhalt auf gehostete Cacheserver (optional)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie die Erstellung von Inhaltsinformationen, auch als Hashes bezeichnet, auf BranchCache-aktivierten Web-und Dateiservern erzwingen. Sie können auch die Daten auf Datei-und Webservern in Paketen zusammenfassen, die auf Remote gehostete Cache Server übertragen werden können.  Dadurch haben Sie die Möglichkeit, Inhalte auf Remote gehosteten Cache Servern vorab zu laden, damit die Daten für den ersten Client Zugriff verfügbar sind.  
  
Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
### <a name="to-prehash-content-and-preload-the-content-on-hosted-cache-servers"></a>So versehen Sie Inhalt vorab und laden den Inhalt auf gehosteten Cache Servern vorab  
  
1.  Melden Sie sich bei der Datei oder dem Webserver an, die die Daten enthält, die Sie vorab laden möchten, und identifizieren Sie die Ordner und Dateien, die Sie auf einem oder mehreren Remote gehosteten Cache Servern laden möchten.  
  
2.  Führen Sie Windows PowerShell als Administrator aus. Führen Sie für jeden Ordner und jede Datei entweder den Befehl "`Publish-BCFileContent`" oder den Befehl "`Publish-BCWebContent`" aus, je nach Typ des Inhalts Servers, um die Hash Generierung zu erzeugen und Daten einem Datenpaket hinzuzufügen.  
  
3.  Nachdem alle Daten dem Datenpaket hinzugefügt wurden, exportieren Sie Sie mithilfe des Befehls `Export-BCCachePackage`, um eine Datenpaket Datei zu entwickeln.  
  
4.  Verschieben Sie die Datenpaket Datei auf die Remote gehosteten Cache Server, indem Sie die Datei Übertragungstechnologie auswählen.  FTP, SMB, http, DVD und Portable Festplatten sind alle funktionierenden Transporte.  
  
5.  Importieren Sie die Datenpaket Datei auf den Remote gehosteten Cache Servern mithilfe des Befehls `Import-BCCachePackage`.  
  

