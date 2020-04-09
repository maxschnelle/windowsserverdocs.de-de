---
title: Planen von Benutzerkonten für eine MultiPoint Services-Umgebung
description: Planungsinformationen für Benutzerkonten in Multipoint Services
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: d47be540-e891-47bd-85da-6df4bbf93b2f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 28ee7a1475ec55352fe344842b8df7633abb9137
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853393"
---
# <a name="plan-user-accounts-for-your-multipoint-services-environment"></a>Planen von Benutzerkonten für eine MultiPoint Services-Umgebung
Die beste Methode zum Implementieren von Benutzerkonten in Multipoint Services hängt von der Größe und Komplexität Ihrer Bereitstellung ab:  
  
-   **Lokale Benutzerkonten** : für eine kleine Bereitstellung mit nur wenigen Computern, auf denen multipoind-Dienste und wenige Benutzer ausgeführt werden, ist es möglicherweise am einfachsten, *lokale Benutzerkonten* zu verwenden, die in Multipoint Services erstellt werden. Sie können für jede Person, die das System verwendet, ein einzelnes Konto erstellen oder ein allgemeines Konto für jede Station erstellen, das jeder zum Anmelden verwenden kann. Multipoint Services-Administratoren erstellen und verwalten lokale Benutzerkonten mithilfe von Multipoint-Manager. Bei den lokalen Konten kann es sich um Administratoren mit eingeschränkten Administratorrechten oder um reguläre Benutzer ohne Zugriff auf den Multipoint Services-Desktop oder den Multipoint-Manager handeln.  
  
-   **Domänen Konten** : Wenn in Ihrer Umgebung viele Computer mit Multipoint Services und vielen Benutzern vorhanden sind, ist es wahrscheinlich sinnvoller, eine Active Directory Domain Services \(AD DS\) Domäne einzurichten und *Domänen Benutzerkonten*zu verwenden, die es Benutzern ermöglichen, von einer beliebigen Station in der Domäne aus auf Ihr eigenes Benutzerprofil und ihre eigenen Einstellungen zuzugreifen. Domänen Benutzerkonten müssen von einem Domänen Administrator auf dem Domänen Controller erstellt werden.  
  
> [!NOTE]  
> In den folgenden Abschnitten werden Szenarien erörtert, die Sie möglicherweise für lokale Benutzerkonten in Multipoint Services implementieren. Wenn Sie Domänen Benutzerkonten verwenden, finden Sie weitere Informationen im Szenario "mindestens ein Multipoint-Server in einer Domänen Netzwerkumgebung" in [Beispielszenarien: Multipoint Services-Benutzerkonten](Example-scenarios--MultiPoint-Services-user-accounts.md).  
  
## <a name="planning-local-user-accounts"></a>Planen von lokalen Benutzerkonten  
In den folgenden Abschnitten werden die vor-und Nachteile sowie die Anforderungen für verschiedene Methoden zum Implementieren einzelner oder gemeinsam genutzter lokaler Benutzerkonten in Ihrer Windows-MultiPoint Services-Umgebung berücksichtigt.  
  
### <a name="use-individual-local-user-accounts"></a>Einzelne lokale Benutzerkonten verwenden  
Wenn Sie lokale Benutzerkonten erstellen, haben Sie die Option zwei Ansätze.  Weisen Sie jeden Benutzer einem bestimmten Server zu, auf dem Multipoint Services ausgeführt wird, und erstellen Sie ein einzelnes Konto für jeden Benutzer. Oder erstellen Sie lokale Benutzerkonten für alle Benutzer auf jedem Computer, auf dem Multipoint Services ausgeführt wird. Ein wichtiger Vorteil der Implementierung einzelner Benutzerkonten besteht darin, dass jeder Benutzer über seine eigene Windows-Desktop Darstellung verfügt, die private Ordner zum Speichern von Daten umfasst. 
  
Aus Sicht der Systemverwaltung ist es möglicherweise bequemer, Benutzer einem bestimmten Multipoint Services-Computer zuzuweisen. Wenn Sie z. b. über zwei Multipoint-Server mit jeweils fünf Stationen verfügen, können Sie lokale Benutzerkonten erstellen, wie in der folgenden Tabelle veranschaulicht.  
  
**Tabelle 1: Zuweisen von lokalen Benutzerkonten zu bestimmten Computern, auf denen Multipoint Services ausgeführt wird**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_06|  
|UserAccount_02|UserAccount_07|  
|UserAccount_03|UserAccount_08|  
|UserAccount_04|UserAccount_09|  
|UserAccount_05|UserAccount_10|  
  
In diesem Szenario hat jeder Benutzer ein einzelnes Konto auf einem bestimmten Computer. Daher können sich alle Benutzer, die über ein lokales Konto auf Computer a verfügen, bei Ihrem Konto von einer beliebigen Station anmelden, die mit Computer a verknüpft ist. Diese Benutzer können jedoch nicht auf Ihre Konten zugreifen, wenn Sie eine Station verwenden, die Computer B zugeordnet ist, und umgekehrt. Ein Vorteil dieses Ansatzes besteht darin, dass Benutzer immer Ihre Dateien finden und darauf zugreifen können, indem Sie immer eine Verbindung mit dem gleichen Computer herstellen.  
  
Im Gegensatz dazu ist es auch möglich, einzelne Benutzerkonten auf allen Computern zu replizieren, auf denen Multipoint Services ausgeführt wird, wie in der folgenden Tabelle veranschaulicht.  
  
**Tabelle 2: Replizieren von Benutzerkonten auf allen Computern, auf denen Multipoint Services ausgeführt wird**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|UserAccount_01|UserAccount_01|  
|UserAccount_02|UserAccount_02|  
|UserAccount_03|UserAccount_03|  
|UserAccount_04|UserAccount_04|  
|UserAccount_05|UserAccount_05|  
  
Ein Vorteil dieses Ansatzes besteht darin, dass Benutzer über ein lokales Benutzerkonto für alle verfügbaren Multipoint Services verfügen. Dieser Vorteil kann jedoch durch die Nachteile aufwiegen. Wenn z. b. der Benutzername und das Kennwort für eine bestimmte Person auf beiden Computern identisch sind, sind die Konten nicht miteinander verknüpft. Wenn sich ein Benutzer am Montag bei seinem Konto auf Computer a anmeldet, speichert eine Datei und meldet sich dann bei seinem Konto auf Computer B am Dienstag an, und er kann nicht auf die Datei zugreifen, die zuvor auf Computer a gespeichert wurde. Darüber hinaus erhöht die Replikation von Benutzerkonten auf mehreren Computern den Verwaltungsaufwand und die Speicheranforderungen.  
  
### <a name="use-generic-local-user-accounts"></a>Generische lokale Benutzerkonten verwenden  
Wenn Ihr Multipoint Services-System nicht mit einer Domäne verbunden ist und Sie kein einzelnes Konto für jeden Benutzer erstellen möchten, können Sie für jede Station generische Konten erstellen. Wenn Sie beispielsweise über zwei Computer verfügen, auf denen Multipoint Services ausgeführt wird, und jedem Computer fünf Stationen zugeordnet sind, können Sie Benutzerkonten erstellen, die den in der folgenden Tabelle aufgeführten ähneln.  
  
**Tabelle 3: Erstellen von generischen Benutzerkonten, einem Konto pro Station**  
  
|Computer A|Computer B|  
|--------------|--------------|  
|Computer_A Station_01|Computer_B Station_01|  
|Computer_A Station_02|Computer_B Station_02|  
|Computer_A Station_03|Computer_B Station_03|  
|Computer_A Station_04|Computer_B Station_04|  
|Computer_A Station_05|Computer_B Station_05|  
  
In diesem Szenario hat jedes Stationskonto das gleiche Kennwort, und sowohl die Kenn Wörter als auch die Namen der generischen Benutzerkonten sind für alle Benutzer verfügbar. Ein Vorteil dieses Ansatzes besteht darin, dass der Aufwand für die Verwaltung von Benutzerkonten wahrscheinlich weniger als bei der Verwendung einzelner Konten ist, weil es in der Regel weniger Stationen als Benutzer gibt. Außerdem wird der Aufwand, der durch das Replizieren von Benutzerkonten auf jedem Server verursacht wird, beseitigt.  
  
Eine andere Möglichkeit ist das Erstellen von generischen Konten auf jedem Server. Jeder Benutzer meldet sich als dasselbe Konto bei einem Server an. Um dies zuzulassen, müssen Sie mehrere Sitzungen pro Konto aktivieren. Sie können weitere vereinfachen, indem Sie den gleichen Kontonamen und das gleiche Kennwort auf allen Servern verwenden. Dies vereinfacht die Anmeldung für die Benutzer, die nur einen Kontonamen und ein Kennwort kennen müssen, damit eine beliebige Station auf einem beliebigen Server verwendet werden kann. Beachten Sie, dass in diesem Szenario alle Benutzer jede beliebige Änderung sehen können. Wenn eine Datei z. b. auf dem Desktop gespeichert wird, können alle Benutzer die Datei sehen.  
  
> [!IMPORTANT]  
> Es ist wichtig zu wissen, dass Benutzer, die auf dem Server gespeichert sind (entweder eine pro Server oder eine pro Station), auf dem Server gespeicherte Dateien – auch in eigenen Dokumenten gespeicherte Dateien nicht privat sind. Jeder Benutzer, der sich mit dem Konto anmeldet, hat Zugriff auf diese Dateien. Wenn Sie ein Konto pro Station verwenden und ein Benutzer auf einer Station Dateien in meinen Dokumenten speichert, hat der Benutzer keinen Zugriff auf diese Dateien auf einer anderen Station. Dasselbe Problem tritt auf, wenn Sie sich bei verschiedenen Multipoint Services-Computern anmelden.  
  
Damit Benutzer von einer beliebigen Station aus auf Ihre Dateien zugreifen können, können Sie einen Dateiserver verwenden, eine Dateifreigabe für jedes Benutzerkonto erstellen oder Benutzern gestatten, Ihre persönlichen Dokumente auf einem USB-Speicherstick oder einem anderen privaten Speichergerät zu speichern. Einzelne USB-Speicherstick ermöglichen einzelnen Benutzern das Speichern privater Dokumente, auch wenn Sie ein Benutzerkonto in einem Multipoint Services-Dienst freigeben.