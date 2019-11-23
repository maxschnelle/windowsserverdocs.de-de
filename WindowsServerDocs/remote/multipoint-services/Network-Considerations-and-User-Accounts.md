---
title: Überlegungen zu Netzwerk und Benutzerkonten
description: Bietet Planungsinformationen für verschiedene Netzwerk-und Benutzer Szenarien mit Multipoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef4859fc-b7ae-4827-ab9c-b1dc07ab6c16
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 5369776a0341bf1f4d4d1d13569cf0964fdf11f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405036"
---
# <a name="network-considerations-and-user-accounts"></a>Überlegungen zu Netzwerk und Benutzerkonten
Multipoint Services können in einer Vielzahl von Netzwerkumgebungen bereitgestellt werden, und es können lokale Benutzerkonten und Domänen Benutzerkonten unterstützt werden. Im Allgemeinen werden Multipoint Services-Benutzerkonten in einer der folgenden Netzwerkumgebungen verwaltet:  
  
-   Einen einzelnen Computer, auf dem Multipoint Services mit lokalen Benutzerkonten ausgeführt wird  
  
-   Mehrere Computer, auf denen Multipoint Services ausgeführt wird, jeweils mit einem lokalen Benutzerkonto  
  
-   Mehrere Computer, auf denen Multipoint Services ausgeführt wird und die Domänen Benutzerkonten verwenden

Definitionsgemäß können auf *lokale Benutzerkonten* nur von dem Computer aus zugegriffen werden, auf dem Sie erstellt wurden. Lokale Benutzerkonten sind Benutzerkonten, die auf einem bestimmten Computer erstellt werden, auf dem Multipoint Services ausgeführt wird. Im Gegensatz dazu sind *Domänen Benutzerkonten* Benutzerkonten, die sich auf einem Domänen Controller befinden, und auf Sie kann von jedem Computer aus zugegriffen werden, der mit der Domäne verbunden ist. Berücksichtigen Sie Folgendes, wenn Sie entscheiden, welche Art von Netzwerkumgebung Sie verwenden möchten:  
  
-   Werden Ressourcen von Servern gemeinsam genutzt?  
  
-   Werden Benutzer zwischen Servern wechseln?  
  
-   Greifen Benutzer auf Datenbankserver zu, die eine Authentifizierung erfordern?  
  
-   Werden Benutzer auf interne Webserver zugreifen, für die eine Authentifizierung erforderlich ist?  
  
-   Ist bereits eine Active Directory Domänen Infrastruktur vorhanden?  
  
-   Wer verwendet die Multipoint Manager-Konsole zum Verwalten von Benutzer Desktops, zum Anzeigen von Miniaturansichten, zum Hinzufügen von Benutzern, zum Einschränken von Websites usw. Verwaltet diese Person mehr als einen Server? Diese Person muss über Administrator Berechtigungen auf den Servern verfügen.  
  
In den folgenden Abschnitten wird die Benutzerkonten Verwaltung in diesen Netzwerkumgebungen behandelt.  
  
## <a name="single-multipoint-server-with-local-user-accounts"></a>Einzelner Multipoint-Server mit lokalen Benutzerkonten  
In Umgebungen mit einem einzelnen Computer, auf dem Multipoint Services ausgeführt wird, muss kein Netzwerk vorhanden sein. Um Internet Ressourcen zu nutzen, sind die Netzwerk Anforderungen jedoch möglicherweise so einfach wie ein Router und eine Verbindung mit einem Internetdienstanbieter (Internet Service Provider, ISP). Netzwerkverbindungen, die einem Netzwerkadapter in Multipoint Services zugeordnet sind, werden standardmäßig so konfiguriert, dass automatisch eine IP-Adresse und DNS-Server Adresse über DHCP abgerufen werden. Internet Router werden in der Regel als DHCP-Server konfiguriert und stellen privaten IP-Adressen für Computer bereit, die eine Verbindung mit dem internen Netzwerk herstellen. Daher können von einem einzelnen Computer, auf dem Multipoint Services ausgeführt wird, eine Verbindung mit der internen Schnittstelle des Routers hergestellt, automatische IP-Informationen abgerufen und eine Verbindung mit dem Internet hergestellt werden, ohne dass ein Administrator einen erheblichen Aufwand oder eine andere Konfiguration durchführt.  
  
Eine gängige Methode zum Verwalten von Benutzern in dieser Art von Umgebung ist das Erstellen eines lokalen Benutzerkontos für jede Person, die auf das System zugreift. Jeder Benutzer, der über ein lokales Benutzerkonto auf diesem Computer verfügt, kann sich von jeder Station, die dem System zugeordnet ist, bei Multipoint Services anmelden. Lokale Benutzerkonten können über den Multipoint-Manager erstellt und verwaltet werden.  
  
## <a name="multiple-multipoint-server-systems-with-local-user-accounts"></a>Mehrere Multipoint-Server Systeme mit lokalen Benutzerkonten  
Da auf lokale Benutzerkonten nur von dem Computer aus zugegriffen werden kann, auf dem Sie erstellt wurden, können Sie lokale Benutzerkonten auf zwei Arten verwalten, wenn Sie mehrere Multipoint Services-Systeme in einer Umgebung bereitstellen:  
  
-   Sie können Benutzerkonten für bestimmte Personen auf bestimmten Computern erstellen, auf denen Multipoint Services ausgeführt wird.  
  
-   Mit dem Multipoint-Manager können Sie Konten für jeden Benutzer auf jedem Computer erstellen, auf dem Multipoint Services ausgeführt wird.  
  
Wenn Sie z. b. die Zuweisung von Benutzern zu einem bestimmten Computer planen, auf dem Multipoint Services ausgeführt wird, können Sie auf Computer a (USER01, user02, user03 und user04) und vier lokalen Benutzerkonten auf Computer B (user05, user06, user07 und user08) vier lokale Benutzerkonten erstellen. In diesem Szenario können sich Benutzer 01\-04 von jeder Station, die mit ihr verbunden ist, bei Computer A anmelden. Sie können sich jedoch nicht bei Computer B anmelden. Dasselbe gilt für Benutzer 05\-08, die sich nur bei Computer B anmelden können, jedoch nicht bei Computer A. je nach der jeweiligen Bereitstellungs Umgebung kann dies akzeptabel oder sogar wünschenswert sein.  
  
Wenn sich allerdings alle Benutzer in der Lage sein müssen, sich bei einem Computer anzumelden, auf dem Multipoint Services ausgeführt wird, muss ein lokales Benutzerkonto für jeden Benutzer auf jedem Computer erstellt werden, auf dem Multipoint Services ausgeführt wird. Wenn Sie die Benutzer auf diese Weise verwalten, werden bestimmte Komplexitäten eingeführt. Wenn sich z. B. USER01 am Montag an Computer a anmeldet und eine Datei im Ordner Dokumente speichert und sich der Benutzer dann am Dienstag an Computer b anmeldet, ist die Datei, die im Ordner Dokumente auf Computer A gespeichert wurde, auf Computer b nicht verfügbar.  
  
Außerdem gibt es keine Möglichkeit, die Kenn Wörter für die Konten automatisch zu synchronisieren, wenn ein Benutzer über Konten auf Computer a und Computer B verfügt. Dies kann dazu führen, dass Benutzer Probleme bei der Anmeldung haben, wenn das Konto Kennwort auf einem Computer geändert wird, nicht jedoch auf dem anderen. Sie können die Benutzerkonten Verwaltung in dieser Art von Netzwerkumgebung vereinfachen, indem Sie jeden Benutzer einem einzelnen Computer zuweisen, auf dem Multipoint Services ausgeführt wird. Auf diese Weise kann sich der Benutzer an allen Stationen anmelden, die diesem Computer zugeordnet sind, und auf die entsprechenden Dateien zugreifen.  
  
## <a name="multiple-multipoint-services-systems-with-domain-accounts"></a>Mehrere Multipoint Services-Systeme mit Domänen Konten  
Domänen Umgebungen sind in großen Netzwerkumgebungen üblich, die mehrere Server umfassen. Beispielsweise können Sie einem oder mehreren Computern, auf denen die Multipoint Services-Rolle ausgeführt wird, eine Domäne hinzufügen und dann Microsoft Active Directory zum Verwalten von Benutzerkonten verwenden, auf die von jedem Computer in der Domäne zugegriffen werden kann. Dadurch können einzelne Domänen Benutzerkonten erstellt werden, und der Zugriff erfolgt über eine beliebige Station in jedem Multipoint Services-System, das der Domäne beigetreten ist.  
 
Wenn Sie Multipoint Services in einer Domänen Umgebung bereitstellen, müssen Sie mehrere Faktoren berücksichtigen:  
  
-   Wenn Domänen Konten verwendet werden, können Sie nicht über den Multipoint-Manager verwaltet werden.  
  
-   Standardmäßig ist Multipoint Services so konfiguriert, dass jeder Benutzer die Berechtigung erhält, sich jeweils nur an einer Station anzumelden. Wenn Sie es Benutzern ermöglichen, sich gleichzeitig mit einem einzelnen Konto bei mehreren Stationen anzumelden, können Sie die Option **Server Einstellungen bearbeiten** im Multipoint-Manager verwenden.  
  
-   Der Speicherort von Domänen Controllern kann sich auf die Geschwindigkeit und Zuverlässigkeit auswirken, mit der sich Benutzer bei der Domäne authentifizieren und Ressourcen suchen können.  
  
## <a name="single-user-account-for-multiple-stations"></a>Einzelnes Benutzerkonto für mehrere Stationen  
Multipoint Services bietet die Möglichkeit, sich mit einem einzelnen Benutzerkonto gleichzeitig an mehreren Stationen auf demselben Computer anzumelden. Diese Funktion ist nützlich in Umgebungen, in denen Benutzer keine eindeutigen Benutzernamen haben und die Verwendung eines einzelnen Benutzerkontos die Verwaltung des Multipoint Services-Systems vereinfachen kann.  
  
