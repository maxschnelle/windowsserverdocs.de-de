---
title: Überlegungen zu Netzwerk und Benutzerkonten
description: Bietet Planungsinformationen für verschiedene Szenarien für Netzwerk und Benutzer mit MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef4859fc-b7ae-4827-ab9c-b1dc07ab6c16
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 9133f28d2c3b36b18a2b6bc81d238835156bf447
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880801"
---
# <a name="network-considerations-and-user-accounts"></a>Überlegungen zu Netzwerk und Benutzerkonten
MultiPoint-Dienste können in verschiedenen netzwerkumgebungen bereitgestellt werden, und können lokale Benutzerkonten und Benutzerkonten der Quelldomäne unterstützt. MultiPoint Services-Benutzerkonten werden in der Regel in einem der folgenden netzwerkumgebungen verwaltet werden:  
  
-   Ein einzelner Computer mit MultiPoint-Dienste mit lokalen Benutzerkonten  
  
-   Mehrere Computer mit MultiPoint-Dienste, und jeder mit einem lokalen Benutzerkonto  
  
-   Mehrere Computer mit MultiPoint Services und die verwenden Benutzerkonten der Quelldomäne

Definitionsgemäß *lokale Benutzerkonten* kann nur zugegriffen werden, auf dem Computer, auf dem sie erstellt wurden. Lokale Benutzerkonten sind Benutzerkonten, die auf einem bestimmten Computer erstellt werden, die MultiPoint Services ausgeführt wird. Im Gegensatz dazu *Domänenbenutzerkonten* sind Benutzerkonten, die befinden sich auf einem Domänencontroller, und sie die zugegriffen werden können, von einem beliebigen Computer, die mit der Domäne verbunden ist. Bei der Entscheidung, welche Art von Netzwerkumgebung verwenden, beachten Sie Folgendes:  
  
-   Werden Ressourcen zwischen Servern gemeinsam werden genutzt?  
  
-   Werden Benutzer zwischen Servern wechseln?  
  
-   Greifen Benutzer-Datenbankservern, die Authentifizierung benötigen?  
  
-   Greifen Benutzer internen Webservern, die Authentifizierung benötigen?  
  
-   Gibt es eine vorhandene Active Directory-Domäneninfrastruktur vorhanden?  
  
-   Die das MultiPoint-Manager verwendet-Konsole zum Verwalten von Benutzerdesktops, Miniaturansichten anzeigen, Hinzufügen von Benutzern, beschränken Websites zu und so weiter? Wird diese Person mehr als einem Server verwalten? Diese Person muss über Administratorrechte auf den Servern verfügen.  
  
In den folgenden Abschnitten behandelt die Verwaltung von Benutzerkonten in diese netzwerkumgebungen.  
  
## <a name="single-multipoint-server-with-local-user-accounts"></a>MultiPoint Server mit lokalen Benutzerkonten  
In Umgebungen mit einem einzelnen Computer, auf dem MultiPoint Services ausgeführt wird, ist es nicht erforderlich, die über ein Netzwerk verfügen. Um Internetressourcen nutzen zu können, können die netzwerkanforderungen jedoch so Grundlegendes wie ein Router und eine Verbindung mit einem Internetdienstanbieter (ISP) sein. Netzwerkverbindungen, die einen Netzwerkadapter in MultiPoint Services zugeordnet sind werden konfiguriert, wird standardmäßig eine IP-Adresse und DNS-Serveradresse automatisch über DHCP abgerufen. Internet-Router in der Regel als DHCP-Server konfiguriert sind, und bieten private IP-Adressen für Computer, die auf dem internen Netzwerk herstellen. Ein einzelner Computer mit MultiPoint Services möglicherweise aus diesem Grund kann eine Verbindung mit der internen Schnittstelle des Routers herstellen, erhalten Informationen zur automatischen IP- und Verbinden mit dem Internet ohne erheblichen Aufwand oder Konfiguration von einem Administrator.  
  
Eine gängige Methode zum Verwalten von Benutzern in dieser Art von Umgebung ist die Erstellung ein lokalen Benutzerkontos für jede Person, die auf das System zugreifen. Jemand ein lokales Benutzerkonto auf diesem Computer hat kann mit MultiPoint Services über jede Station anmelden, das mit dem System verknüpft ist. Lokale Benutzerkonten können erstellt und von MultiPoint-Manager verwaltet werden.  
  
## <a name="multiple-multipoint-server-systems-with-local-user-accounts"></a>Mehrere MultiPoint Server-Systeme mit lokalen Benutzerkonten  
Angesichts der Tatsache, dass lokale Benutzerkonten nur von dem Computer aus zugänglich sind, auf denen sie erstellt wurden, wenn Sie mehrere MultiPoint Services-Systeme in einer Umgebung bereitstellen, können Sie lokale Benutzerkonten auf zwei Arten verwalten:  
  
-   Sie können Benutzerkonten erstellen, für bestimmte Personen auf bestimmten Computern, auf dem MultiPoint Services ausgeführt wird.  
  
-   Sie können die MultiPoint-Manager verwenden, zum Erstellen von Konten für jeden Benutzer auf jedem Computer, auf dem MultiPoint Services ausgeführt wird.  
  
Wenn Sie planen, weisen Sie Benutzer zu einem bestimmten Computer, die MultiPoint Services ausgeführt wird, können Sie z. B. vier lokale Benutzerkonten auf Computer A ("user01", user02, Benutzer03 und user04) und vier lokale Benutzerkonten auf Computer B (user05, user06, user07 und user08) erstellen. In diesem Szenario müssen Benutzer-01\-04 können melden Sie sich auf Computer A über jede Station, die mit ihm verbunden ist, aber sie können nicht melden Sie sich an Computer b Das gleiche gilt für Benutzer 05\-08, die nur auf Computer B, aber nicht auf Computer a abhängig, auf die spezielle bereitstellungsumgebung anmelden kann, kann dies akzeptabel oder sogar wünschenswert sein.  
  
Wenn jeder Benutzer anmelden auf den Computern, auf dem MultiPoint Services ausgeführt werden muss, muss jedoch ein lokales Benutzerkonto für jeden Benutzer auf jedem Computer erstellt werden, das MultiPoint Services ausgeführt wird. Zum Verwalten von Benutzern auf diese Weise auswählen, werden bestimmte Komplexitäten eingeführt. Wenn z. B. "user01" auf Computer A am Montag anmeldet und speichert eine Datei im Ordner "Dokumente", und klicken Sie dann die Benutzer meldet sich an Computer B am Dienstag, die Datei, die im Ordner "Dokumente" auf Computer A gespeichert wurde für die nicht zugegriffen werden kann, auf Computer b.  
  
Darüber hinaus verfügt ein Benutzer über Konten auf Computer A und B des Computers, gibt es keine Möglichkeit für die automatische Synchronisierung der Kennwörter für Konten. Dadurch können Benutzer, die schwierigkeiten mit der Anmeldung das Kennwort für das auf einem Computer, aber nicht in der anderen geändert werden soll. Sie können die Verwaltung von Benutzerkonten in dieser Art von Umgebung vereinfachen, durch Zuweisen von jedem Benutzer zu einem einzelnen Computer, auf dem MultiPoint Services ausgeführt wird. Auf diese Weise kann der Benutzer auf die Stationen melden Sie sich, die mit dem betreffenden Computer zugeordnet sind und Zugriff auf die entsprechenden Dateien.  
  
## <a name="multiple-multipoint-services-systems-with-domain-accounts"></a>Mehrere MultiPoint Services-Systeme mit Domänenkonten  
Domänenumgebungen sind häufig in großen netzwerkumgebungen, die mehrere Server enthalten. Sie können z. B. einem oder mehreren Computern, die mit dem MultiPoint Services-Rolle zu einer Domäne beitreten und dann Microsoft Active Directory verwenden, um Benutzerkonten zu verwalten, die von einem beliebigen Computer in der Domäne zugegriffen werden kann. Dadurch können für einzelne Domänenbenutzerkonten erstellt und jedes MultiPoint Services-System, das mit der Domäne verknüpft ist über jede Station zugegriffen werden.  
 
Wenn Sie in einer domänenumgebung MultiPoint Services bereitstellen, gibt es mehrere Faktoren zu berücksichtigen:  
  
-   Wenn Domänenkonten verwendet werden, können sie vom MultiPoint-Manager verwaltet werden.  
  
-   MultiPoint Services wird standardmäßig so konfiguriert, um jedem Benutzer die Berechtigung zu einem Zeitpunkt nur eine Station anmelden zu ermöglichen. Wenn Sie sich entscheiden, dass Benutzer mithilfe eines einzelnen Kontos gleichzeitig an mehreren Stationen anmelden können, können Sie mithilfe der **servereinstellungen bearbeiten** Option im MultiPoint-Manager.  
  
-   Der Speicherort der Domänencontroller möglicherweise Auswirkungen auf die Geschwindigkeit und Zuverlässigkeit, die mit dem Benutzer werden zur Authentifizierung mit der Domäne, und suchen Sie nach Ressourcen können.  
  
## <a name="single-user-account-for-multiple-stations"></a>Einzelnes Benutzerkonto für mehrere Stationen  
MultiPoint Services hat die Möglichkeit, die an mehreren Stationen auf dem gleichen Computer gleichzeitig mit einem einzigen Benutzerkonto anmelden. Dieses Feature eignet sich in Umgebungen, in denen Benutzer eindeutige Benutzernamen nicht angegeben werden, und mit einem einzigen Benutzerkonto anmelden, die Verwaltung von MultiPoint Services-Systems vereinfachen kann.  
  
