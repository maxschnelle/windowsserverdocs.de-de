---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: Erstellen eines Entwurfs für Standortverknüpfungen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: fdff477a1fb7cbe42402b2bb608eea55f2f9ec09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402704"
---
# <a name="creating-a-site-link-design"></a>Erstellen eines Entwurfs für Standortverknüpfungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellen Sie einen Standort Verknüpfungs Entwurf, um Ihre Standorte mit Standort Verknüpfungen zu verbinden. Standort Verknüpfungen reflektieren die standortübergreifende Konnektivität und Methode zum Übertragen von Replikations Datenverkehr. Sie müssen Standorte mit Standort Verknüpfungen verbinden, damit die Domänen Controller an jedem Standort Active Directory Änderungen replizieren können.  
  
## <a name="connecting-sites-with-site-links"></a>Verbinden von Standorten mit Standortverknüpfungen

Um Standorte mit Standort Verknüpfungen zu verbinden, identifizieren Sie die Mitgliedsstandorte, die Sie mit der Standort Verknüpfung verbinden möchten, erstellen Sie ein Standort Verknüpfungs Objekt in dem entsprechenden standortübergreifenden Transportcontainer, und benennen Sie die Standort Verknüpfung. Nachdem Sie die Standort Verknüpfung erstellt haben, können Sie mit dem Festlegen der Standort Verknüpfungs Eigenschaften fortfahren.  
  
Wenn Sie Standort Verknüpfungen erstellen, stellen Sie sicher, dass jeder Standort in einer Standort Verknüpfung enthalten ist. Stellen Sie darüber hinaus sicher, dass alle Standorte über andere Standort Verknüpfungen miteinander verbunden sind, damit die Änderungen von Domänen Controllern an allen Standorten repliziert werden können. Wenn Sie dies nicht tun, wird im Verzeichnisdienst Ereignisanzeige Protokoll eine Fehlermeldung mit dem Hinweis generiert, dass die Standort Topologie nicht verbunden ist.  
  
Wenn Sie Websites zu einer neu erstellten Standort Verknüpfung hinzufügen, stellen Sie fest, ob der hinzugefügte Standort Mitglied anderer Standort Verknüpfungen ist, und ändern Sie bei Bedarf die Standort Verknüpfungs Mitgliedschaft des Standorts. Wenn Sie z. b. einen Standort als Mitglied der Standard-First-Site-Verknüpfung festlegen, wenn Sie den Standort erstmalig erstellen, achten Sie darauf, dass Sie den Standort aus dem Standard-First-Site-Link entfernen, nachdem Sie den Standort einer neuen Standort Verknüpfung hinzugefügt haben. Wenn Sie den Standort nicht aus dem Standard-First-Site-Link entfernen, trifft die Konsistenzprüfung (KCC) Routing Entscheidungen auf Grundlage der Mitgliedschaft beider Standort Verknüpfungen, was zu einem falschen Routing führen kann.  
  
Verwenden Sie die Liste der Standorte und verknüpften Speicherorte, die Sie im Arbeitsblatt "geografische Standorte und Kommunikations Links" (DSSTOPO_1. doc) notiert haben, um die Mitgliedsstandorte zu identifizieren, die Sie mit einer Standort Verknüpfung verbinden möchten. Wenn mehrere Standorte die gleiche Konnektivität und Verfügbarkeit aufweisen, können Sie Sie mit derselben Standort Verknüpfung verbinden.  
  
Der Container für standortübergreifende Transporte bietet die Möglichkeit zum Mapping von Standort Verknüpfungen zu dem Transport, den der Link verwendet. Wenn Sie ein Standort Verknüpfungs Objekt erstellen, erstellen Sie es entweder in dem IP-Container, der die Standort Verknüpfung mit dem Remote Prozedur Aufruf (RPC) über IP-Transport verknüpft, oder mit dem Simple Mail Transfer Protocol (SMTP)-Container, der die Standort Verknüpfung dem SMTP zuordnet. Personen.  
  
> [!NOTE]  
> Die SMTP-Replikation wird in zukünftigen Versionen von Active Directory Domain Services (AD DS) nicht unterstützt. Daher wird das Erstellen von Standort Verknüpfungs Objekten im SMTP-Container nicht empfohlen.  
  
Wenn Sie ein Standort Verknüpfungs Objekt im entsprechenden standortübergreifenden Transportcontainer erstellen, verwendet AD DS RPC-over-IP, um die standortübergreifende und Standort interne Replikation zwischen Domänen Controllern zu übertragen. Um Daten während der Übertragung sicher zu halten, verwendet die RPC-over-IP-Replikation sowohl das Kerberos-Authentifizierungsprotokoll als auch die Datenverschlüsselung  
  
Wenn keine direkte IP-Verbindung verfügbar ist, können Sie die Replikation Zwischenstand Orten für die Verwendung von SMTP konfigurieren. Die SMTP-Replikations Funktionalität ist jedoch begrenzt und erfordert eine Unternehmens Zertifizierungsstelle (Certification Authority, ca). SMTP kann nur die Konfigurations-, Schema-und Anwendungsverzeichnis Partitionen replizieren. die Replikation von Domänen Verzeichnis Partitionen wird nicht unterstützt.  
  
Verwenden Sie zum Benennen von Standort Verknüpfungen ein konsistentes Benennungs Schema, z. b. name_of_site1-name_of_site2. Notieren Sie die Liste der Standorte, verknüpften Sites und die Namen der Standort Verknüpfungen, die diese Standorte in einem Arbeitsblatt verbinden. Ein Arbeitsblatt, das Sie beim Aufzeichnen von Standortnamen und verknüpften Standort Verknüpfungs Namen unterstützt, finden Sie unter [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Herunterladen von Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip und Öffnen von "Websites und Zugehörige Standort Verknüpfungen "(DSSTOPO_5. doc).  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung

[Festlegen von Standortverknüpfungseigenschaften](Setting-Site-Link-Properties.md)  
