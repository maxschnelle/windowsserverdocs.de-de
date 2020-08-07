---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: dea774dbacb195ede158137eb6c888408fd1084f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947657"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Hinzufügen eines Hostressourceneintrags (A) zum Unternehmens-DNS für einen Verbundserver



Damit Clients im Unternehmensnetzwerk mithilfe der integrierten Windows-Authentifizierung erfolgreich auf einen Verbund Server zugreifen können, \( \) muss zunächst ein Ressourcen Daten Satz für einen Host in der Unternehmens Domain Name System DNS erstellt werden, \( \) der den Hostnamen des Konto Verbund Servers auflöst \( , z \) . b. fs.fabrikam.com in die IP-Adresse des Verbund Servers oder des Verbund Server Clusters. Mit dem folgenden Verfahren können Sie dem Unternehmens- \( \) DNS für einen Verbund Server einen Host einen Ressourcen Daten Satz hinzufügen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>So fügen Sie dem \( \) Unternehmens-DNS einen Ressourcen Daten Satz für einen Verbund Server hinzu

1.  Öffnen Sie auf einem DNS-Server für das Unternehmensnetzwerk das DNS-Snap- \- in.

2.  Klicken Sie in der Konsolen Struktur mit \- der rechten Maustaste auf die entsprechende Forward-Lookupzone, und klicken Sie dann auf **neuer Host \( A oder AAAA \) **.

3.  Geben Sie unter **Name**nur den Computernamen des Verbund Servers oder des Verbund Server Clusters ein. Geben Sie z. b. für den voll qualifizierten Domänen Namen \( FQDN \) FS.fabrikam.com **FS**ein.

4.  Geben Sie unter **IP-Adresse**die IP-Adresse für den Verbund Server oder Verbund Server Cluster ein, z. b. 192.168.1.4.

5.  Klicken Sie auf **Host hinzufügen**.

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)

[Namensauflösungsanforderungen für Verbundserver](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))

