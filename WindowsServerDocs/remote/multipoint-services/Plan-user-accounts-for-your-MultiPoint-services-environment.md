---
title: Planen von Benutzerkonten für eine MultiPoint Services-Umgebung
description: Informationen zur Planung für Benutzerkonten in MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d47be540-e891-47bd-85da-6df4bbf93b2f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 02862c1a317dfe5deff75be4a80595c8dc8bc3f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864171"
---
# <a name="plan-user-accounts-for-your-multipoint-services-environment"></a>Planen von Benutzerkonten für eine MultiPoint Services-Umgebung
Die beste Möglichkeit zum Implementieren von Benutzerkonten in MultiPoint Services hängt von der Größe und Komplexität der Bereitstellung ab:  
  
-   **Lokale Benutzerkonten** – für eine kleine Bereitstellung mit nur wenigen Computern ausgeführten MultiPoind Dienste und einigen Benutzern unter Umständen am einfachsten mit *lokale Benutzerkonten* , die in MultiPoint Services erstellt werden. Sie können ein einzelnes Konto für jede Person erstellen, die das System verwendet wird, oder erstellen Sie ein allgemeines Konto für jede Station, die jeder Benutzer zum Anmelden verwenden können. MultiPoint Services-Administratoren erstellen und Verwalten von lokalen Benutzerkonten mit dem MultiPoint-Manager. Die lokalen Konten können Administratoren sein, über Administratorrechte nur über begrenzte oder werden reguläre Benutzer ohne Zugriff auf die MultiPoint Services-Desktop oder eine MultiPoint-Manager.  
  
-   **Domänenkonten** -weist Ihre Umgebung auf zahlreichen Computern mit MultiPoint Services und viele Benutzer, Sie werden wahrscheinlich ist es sinnvoller, eine Active Directory Domain Services einrichten \(AD DS\) Domänen- und Verwendung *Domänenbenutzerkonten*, die ermöglichen, dass eines Benutzers sein eigenes Benutzerdateien und-Einstellungen über jede Station in der Domäne den Zugriff auf. Domänenbenutzerkonten müssen auf dem Domänencontroller von einem Domänenadministrator erstellt werden.  
  
> [!NOTE]  
> Den folgenden Abschnitten werden Szenarien, die Sie für lokale Benutzerkonten in MultiPoint Services implementieren können. Wenn Sie Domänenbenutzerkonten verwenden, finden Sie unter "einen oder mehrere MultiPoint Server in einer Netzwerkumgebung für die Domäne" Szenario in [Beispielszenarien: MultiPoint Services-Benutzerkonten](Example-scenarios--MultiPoint-Services-user-accounts.md).  
  
## <a name="planning-local-user-accounts"></a>Planen der lokalen Benutzerkonten  
In den folgenden Abschnitten betrachten Sie die Vorteile, Nachteile und Anforderungen für mehrere Möglichkeiten, die einzeln oder gemeinsam genutzten lokalen Benutzerkonten in Ihrer Windows MultiPoint Services-Umgebung zu implementieren.  
  
### <a name="use-individual-local-user-accounts"></a>Verwenden Sie die einzelnen lokalen Benutzerkonten  
Wenn Sie lokale Benutzerkonten erstellen zu können, müssen Sie die Option zwei Ansätze.  Weisen Sie jedem Benutzer mit einem bestimmten Server, dem MultiPoint Services ausgeführt wird, und erstellen ein einzelnes Konto für jeden Benutzer. Oder erstellen Sie lokale Benutzerkonten für alle Benutzer auf jedem Computer, auf dem Multipoint Services ausgeführt wird. Ein wichtiger Vorteil der einzelne Benutzerkonten zu implementieren ist, dass jeder Benutzer verfügt über ein eigenes Windows-desktopdarstellung, die private Ordner zum Speichern von Daten enthält. 
  
Vom Standpunkt Management System kann das Zuweisen von Benutzern zu einem bestimmten MultiPoint Server-Computer besser geeignet sein. Z. B. Wenn Sie zwei MultiPoint Server mit fünf Stationen verfügen, können Sie lokale Benutzerkonten erstellen, wie in der folgenden Tabelle dargestellt.  
  
**Tabelle 1: Zuweisen von lokalen Benutzerkonten auf bestimmte Computer, auf dem MultiPoint Services ausgeführt wird**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_06|  
|UserAccount_02|UserAccount_07|  
|UserAccount_03|UserAccount_08|  
|UserAccount_04|UserAccount_09|  
|UserAccount_05|UserAccount_10|  
  
In diesem Szenario verfügt jeder Benutzer ein einzelnes Konto auf einem bestimmten Computer. Aus diesem Grund jeder Benutzer, die ein lokales Konto auf Computer A kann über jede Station mit Computer A. verknüpft ihr oder seinem Konto anmelden verfügt Diese Benutzer jedoch zugreifen nicht ihren Konten, wenn sie eine Station, verknüpft mit Computer B (und umgekehrt) verwenden. Ein Vorteil dieses Ansatzes ist, indem Sie immer auf demselben Computer verbinden, Benutzer können immer finden und Zugriff auf ihre Dateien.  
  
Im Gegensatz dazu ist es auch möglich, einzelne Benutzerkonten auf allen Computern mit MultiPoint Services zu replizieren, wie in der folgenden Tabelle dargestellt.  
  
**Tabelle 2: Replizieren von Benutzerkonten auf allen Computern, auf dem MultiPoint Services ausgeführt wird**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_01|  
|UserAccount_02|UserAccount_02|  
|UserAccount_03|UserAccount_03|  
|UserAccount_04|UserAccount_04|  
|UserAccount_05|UserAccount_05|  
  
Ein Vorteil dieses Ansatzes ist, dass Benutzer ein lokales Benutzerkonto auf jedem verfügbaren MultiPoint-Dienste. Die Nachteile überwiegen jedoch möglicherweise diesen Vorteil. Auch wenn Sie den Benutzernamen und das Kennwort für eine bestimmte Person auf beiden Computern identisch sind, sind z. B. die Konten nicht miteinander verknüpft. Aus diesem Grund, wenn ein Benutzer sich an seinem meldet oder ihr Konto auf Computer A am Montag, speichert eine Datei, und klicken Sie dann meldet sich an seinem Konto auf Computer B am Dienstag, werden er kann nicht zum Zugriff auf die Datei, die zuvor gespeicherte auf Computer A. außerdem , Replizieren von Benutzerkonten auf mehreren Computern wird der administrative Aufwand und speicheranforderungen erhöht.  
  
### <a name="use-generic-local-user-accounts"></a>Verwenden Sie die generische lokale Benutzerkonten  
Wenn Ihre MultiPoint Services-System nicht mit einer Domäne verbunden ist und Sie kein einzelnes Konto für jeden Benutzer erstellen möchten, können Sie allgemeine Konten für jede Station erstellen. Wenn Sie zwei Computer, auf dem MultiPoint Services ausgeführt wird, und fünf Stationen mit allen Computern verknüpft sind, könnten Sie z. B. Benutzerkonten ähneln denen in der folgenden Tabelle zu erstellen.  
  
**Tabelle 3: Erstellen generischer-Benutzerkonten, ein Konto pro station**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|Computer_A-Station_01|Computer_B-Station_01|  
|Computer_A-Station_02|Computer_B-Station_02|  
|Computer_A-Station_03|Computer_B-Station_03|  
|Computer_A-Station_04|Computer_B-Station_04|  
|Computer_A-Station_05|Computer_B-Station_05|  
  
In diesem Szenario wird für jedes Konto Station hat das gleiche Kennwort, und sowohl die generische Benutzernamen für die Kennwörter für alle Benutzer verfügbar sind. Ein Vorteil dieses Ansatzes ist, dass der Mehraufwand für die Verwaltung von Benutzerkonten wahrscheinlich weniger als verwendet werden, wenn einzelne Konten verwenden, da es weniger Stationen als Benutzer in der Regel sind. Darüber hinaus lässt sich der Mehraufwand durch die Replikation von Benutzerkonten auf jedem Server verursacht.  
  
Eine weitere Möglichkeit ist die Erstellung von allgemeinen Konten auf jedem Server. Jeder Benutzer meldet sich mit einem Server unter dem gleichen Konto. Um dies zu ermöglichen, müssen Sie mehrere Sitzungen pro Konto aktivieren. Sie können weiter vereinfachen, indem Sie den gleichen Kontonamen und das Kennwort auf allen Servern mit verwendet wird. Dies vereinfacht die Anmeldung für die Benutzer, die nur einen Kontonamen und das Kennwort jede Station auf einem beliebigen Server kennen müssen. Anzumerken ist, in diesem Szenario alle Benutzer, die jeder Benutzer macht alle Änderungen sehen können. Wenn eine Datei auf dem Desktop gespeichert wird, können alle Benutzer beispielsweise die Datei sehen.  
  
> [!IMPORTANT]  
> Es ist wichtig zu verstehen, dass beim Benutzer, ein Benutzerkonto an, die entweder einer pro Server oder eine einzelne Station freigeben, Dateien, die auf dem Server – sogar Dateien im Ordner Eigene Dateien gespeichert - gespeichert nicht privat sind. Jeder Benutzer, die mit dem Konto anmeldet hat Zugriff auf diese Dateien. Wenn Sie ein Konto pro-Station verwenden, wenn ein Benutzer Dateien, Eigene Dateien auf einer Station speichert, wird der Benutzer nicht auf diese Dateien auf einer anderen Station zugreifen. Dasselbe gilt für die Anmeldung auf andere MultiPoint Server-Computer.  
  
Damit Benutzer auf ihre Dateien über jede Station zugreifen können, können Sie Dateiserver verwenden, eine Dateifreigabe für jedes Benutzerkonto erstellen oder können Benutzer ihre persönlichen Dokumente auf einem USB-Flashlaufwerk oder andere private Speichergerät gespeichert. Einzelne USB-Flashlaufwerke aktivieren Sie einzelne Benutzern um private Dokumente zu speichern, selbst wenn sie ein Benutzerkonto in einem MultiPoint Services gemeinsam nutzen.