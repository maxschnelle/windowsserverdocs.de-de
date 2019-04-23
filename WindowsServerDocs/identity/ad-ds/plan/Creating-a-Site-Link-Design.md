---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: Erstellen eines Entwurfs für Standortverknüpfungen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4e0607cf66d41e1747b108a3ecc10562120d9174
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861931"
---
# <a name="creating-a-site-link-design"></a>Erstellen eines Entwurfs für Standortverknüpfungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen eines Entwurfs für standortverknüpfungen zu Ihren Standorten mit standortverknüpfungen zu verbinden. Standortverknüpfungen wider, die standortübergreifende Konnektivität und die Methode verwendet, um Replikationsdatenverkehr zu übertragen. Sie müssen Standorte mit standortverknüpfungen verbinden, sodass Domänencontroller an jedem Standort Active Directory-Änderungen replizieren können.  
  
## <a name="connecting-sites-with-site-links"></a>Verbinden von Standorten mit Standortverknüpfungen

Identifizieren Sie die Member-Sites, die Sie verwenden möchten, Herstellen einer Verbindung mit der standortverknüpfung, erstellen ein Standortverknüpfungsobjekt im jeweiligen Container standortübergreifende Transporte und geben Sie den Namen der standortverknüpfung, zum Verbinden von Standorten mit standortverknüpfungen. Nach der Erstellung der standortverknüpfung können Sie mit der Website legen Sie Eigenschaften für rollenverknüpfung fortfahren.  
  
Wenn Sie standortverknüpfungen zu erstellen, stellen Sie sicher, dass jeder Standort in eine standortverknüpfung enthalten ist. Darüber hinaus stellen Sie sicher, dass alle Standorte miteinander über andere standortverknüpfungen verbunden sind, damit die Änderungen an allen anderen Standorten von Domänencontrollern an einem beliebigen Standort repliziert werden können. Wenn Sie nicht dies tun, wird eine Fehlermeldung generiert, in das Verzeichnisdienst-Protokoll in der Ereignisanzeige mit dem Hinweis, dass die Standorttopologie nicht verbunden ist.  
  
Wenn Sie eine standortverknüpfung auf neu erstellte Standorte hinzugefügt haben, zu bestimmen Sie, ob der Standort hinzugefügt werden von anderen standortverknüpfungen angehört, und ändern Sie die Standortmitgliedschaft-Link der Website bei Bedarf. Z. B. Wenn Sie einer Website ein Mitglied der Standard-First-Site-Link vornehmen, wenn Sie zu Beginn die Website erstellen, achten Sie darauf, entfernen den Standort aus der Standard-First-Site-Link, nachdem Sie den Standort einer neuen standortverknüpfung hinzugefügt. Wenn Sie den Standort aus der Standard-First-Site-Link nicht entfernen, stellen die Konsistenzprüfung (KCC) Routingentscheidungen auf Basis der Mitgliedschaft von beiden standortverknüpfungen, was falsch routing bewirken würde.  
  
Um die mitgliederstandorte zu identifizieren, die Sie mit einem Standort-Link verbinden möchten, verwenden Sie die Liste der Speicherorte und verknüpfte Standorte, die Sie in das Arbeitsblatt "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc) aufgezeichnet. Wenn mehrere Standorte die gleichen Konnektivität und Verfügbarkeit zueinander haben, können Sie sie mit der gleichen standortverknüpfung verbinden.  
  
Der standortübergreifende Transporte Container bietet die Möglichkeit, für die Zuordnung von standortverknüpfungen an den Transport, den der Link verwendet. Wenn Sie ein Standortverknüpfungsobjekt erstellen, erstellen Sie in der IP--Container, der den Remoteprozeduraufruf (RPC) über IP-Transport die standortverknüpfung zugeordnet, oder den Container Simple Mail Transfer Protocol (SMTP), der damit die standortverknüpfung mit den SMTP-Server verknüpft Transport.  
  
> [!NOTE]  
> SMTP-Replikation wird werden in zukünftigen Versionen von Active Directory Domain Services (AD DS); nicht unterstützt. aus diesem Grund wird das Erstellen von Links Standortobjekte im SMTP-Container nicht empfohlen.  
  
Wenn Sie ein Standortverknüpfungsobjekt im jeweiligen standortübergreifende Transporte Container erstellen, verwendet AD DS RPC über IP sowohl standortübergreifender und standortinterner Replikation zwischen Domänencontrollern zu übertragen. Um Daten bei der Übertragung zu schützen, verwendet RPC-über-IP-Replikation sowohl die Kerberos-Authentifizierung Protokoll- und Verschlüsselung.  
  
Wenn eine direkte IP-Verbindung nicht verfügbar ist, können Sie die Replikation zwischen Standorten zu SMTP konfigurieren. Die SMTP-Replikationsfunktionalität ist jedoch beschränkt und erfordert von einer Unternehmenszertifizierungsstelle (CA). SMTP kann nur die Konfiguration, Schema und Anwendungsverzeichnispartitionen replizieren und die Replikation von Domänenverzeichnispartitionen nicht unterstützt.  
  
Benennen Sie die standortverknüpfungen, verwenden Sie eine konsistente Benennungsschema, z. B. name_of_site1-name_of_site2. Notieren Sie die Liste der Standorte, verknüpften Websites und die Namen der standortverknüpfungen Herstellen einer Verbindung diese Websites in einem Arbeitsblatt ein. Ein Arbeitsblatt, das Sie beim Aufzeichnen von Standortnamen und zugeordnete standortsystemserver Linknamen unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, herunterladen und Öffnen Sie "Standorte und Standortverknüpfungen verknüpft ist" (DSSTOPO_5.doc).  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Festlegen von Standortverknüpfungseigenschaften](Setting-Site-Link-Properties.md)  
