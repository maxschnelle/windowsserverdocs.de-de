---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: "Erstellen eines Entwurfs für Standortverknüpfungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9eb54781035424c9a5210e11fbdeafc55496c6c3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-link-design"></a>Erstellen eines Entwurfs für Standortverknüpfungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Erstellen eines Entwurfs für standortverknüpfungen Ihre Websites mit Links zu Websites zu verbinden. Standortverknüpfungen Rechnung zu tragen die standortübergreifende Konnektivität und die Methode zum Übertragen von Replikationsdatenverkehr verwendet. Sie müssen Standorten mit standortverknüpfungen verbinden, sodass Änderungen an Active Directory-Domänencontroller an jedem Standort repliziert werden können.  
  
## <a name="connecting-sites-with-site-links"></a>Verbinden von Standorten mit standortverknüpfungen  
Identifizieren Sie die Member-Websites, die Sie verwenden möchten, verbinden Sie mit der standortverknüpfung, erstellen ein Standortverknüpfungsobjekt im jeweiligen standortübergreifende Transporte Container und geben Sie den Namen des standortverknüpfung zum Verbinden von Standorten mit standortverknüpfungen. Nachdem Sie die standortverknüpfung erstellen, können Sie den Standort Linkeigenschaften festlegen fortfahren.  
  
Wenn Sie Links zu Websites erstellen, stellen Sie sicher, dass jeder Standort in eine standortverknüpfung enthalten ist. Darüber hinaus stellen Sie sicher, dass alle Standorte miteinander über andere standortverknüpfungen verbunden sind, damit die Änderungen an allen anderen Standorten von Domänencontrollern an einem beliebigen Standort repliziert werden können. Wenn Sie dies nicht tun, wird eine Fehlermeldung generiert, in das Verzeichnisdienst-Protokoll in der Ereignisanzeige besagt, dass die Standorttopologie nicht verbunden ist.  
  
Wenn Sie einen Link für neu erstellte Standort Websites hinzufügen, zu bestimmen Sie, ob der Standort hinzugefügt werden Mitglied einer anderen standortverknüpfungen, und ändern Sie die Website-Link-Mitgliedschaft des Standorts bei Bedarf. Wenn Sie einer Website, ein Mitglied der Default-First-Site-Link vornehmen Wenn Sie zunächst den Standort erstellen, werden Sie z.B. sicher, dass den Standort über den Default-First-Site-Link entfernen, nachdem Sie den Standort einer neuen standortverknüpfung hinzugefügt. Wenn Sie die Website nicht über den Default-First-Site-Link entfernen, stellen (Knowledge Consistency Checker, KCC) Routingentscheidungen basierend auf der Mitgliedschaft der beiden standortverknüpfungen, was zu falschen Routing führen kann.  
  
Um die Member Standorte zu identifizieren, die Sie mit einem Link Standort eine Verbindung herstellen möchten, verwenden Sie die Liste der Speicherorte und verknüpfte Standorte, die Sie im Arbeitsblatt (DSSTOPO_1.doc) "Geografische Standorte und Kommunikationsverbindungen" aufgezeichnet. Wenn mehrere Standorte die gleichen Konnektivität und Verfügbarkeit miteinander verfügen, können Sie diese mit dem gleichen Standort Link verbinden.  
  
Der standortübergreifende Transporte Container bietet die Möglichkeit, für die Zuordnung von standortverknüpfungen zu den Transport an, dem der Link verwendet. Wenn Sie ein Standortverknüpfungsobjekt erstellen, erstellen Sie es in der IP-Container, der die standortverknüpfung mit der Remoteprozeduraufruf (RPC) über IP-Transport verknüpft werden soll, oder den Container Simple Mail Transfer Protokoll (SMTP), des SMTP-Transports die standortverknüpfung zuordnet.  
  
> [!NOTE]  
> SMTP-Replikation wird werden in zukünftigen Versionen von Active Directory-Domänendienste (AD DS); nicht unterstützt. Erstellen von Standortobjekten-Links im Container SMTP wird daher nicht empfohlen.  
  
Wenn Sie ein Standortverknüpfungsobjekt im jeweiligen standortübergreifende Transporte Container erstellen, verwendet AD DS RPC über IP standortübergreifende und standortinterne Replikation zwischen Domänencontrollern zu übertragen. Um Daten auf dem Weg zu gewährleisten, wird von RPC über IP-Replikation sowohl die Kerberos-Authentifizierung und Verschlüsselung verwendet.  
  
Wenn eine direkte IP-Verbindung nicht verfügbar ist, können Sie die Replikation zwischen Standorten mit SMTP konfigurieren. Allerdings die SMTP-Replikationsfunktionalität ist begrenzt und muss von einer Unternehmenszertifizierungsstelle (CA). SMTP kann nur die Konfiguration, Schema und Anwendungsverzeichnispartitionen replizieren und die Replikation von Domänenverzeichnispartitionen wird nicht unterstützt.  
  
Nennen Sie Links zu Websites, verwenden Sie einen konsistenten Benennungsschema, z.B. name_of_site1 name_of_site2. Notieren Sie die Liste der Websites, verlinkten Websites und die Namen der standortverknüpfungen, die diesen Standorten in einem Arbeitsblatt zu verbinden. Ein Arbeitsblatt, die Ihnen bei der Aufzeichnung Standortnamen und zugehörigen Link Standortnamen, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und Öffnen Sie "-Standorte und Standortverknüpfungen verknüpft" (DSSTOPO_5.doc).  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
[Festlegen von Standortverknüpfungseigenschaften](Setting-Site-Link-Properties.md)  
  


