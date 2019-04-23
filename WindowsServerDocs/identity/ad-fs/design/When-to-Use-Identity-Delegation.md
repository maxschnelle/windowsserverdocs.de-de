---
ms.assetid: 6e711a96-9055-4508-b6d4-318d6aa95fd1
title: Anwendungsbereiche für Identitätsdelegierung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: af227d9e87ddb73f194dd46c8ce45fcdf12a34cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872551"
---
# <a name="when-to-use-identity-delegation"></a>Anwendungsbereiche für Identitätsdelegierung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
  
## <a name="what-is-identity-delegation"></a>Was ist Identitätsdelegierung?  
Identitätsdelegierung ist ein Feature von Active Directory Federation Services \(AD FS\) , die Administrator kann\-angegebenen Konten, um die Identität von Benutzern anzunehmen. Das Konto, das die Identität des Benutzer annimmt, wird als *Delegat* bezeichnet. Diese Delegierungsmöglichkeit ist für viele verteilte Anwendungen entscheidend, bei denen mehrere Zugriffssteuerungsprüfungen nacheinander für jede Anwendung, Datenbank oder jeden Dienst in der Autorisierungskette für die ursprüngliche Anforderung durchgeführt werden müssen. Viele Real\-Szenarien vorhanden sind, in dem muss eine "Front-End"-Webanwendung Abrufen von Daten aus einer sichereren "Back-End", z. B. einen Webdienst, der mit einer Microsoft SQL Server-Datenbank verbunden ist.  
  
Z. B. ein bereits vorhandener Parts\-sortieren die Website kann programmgesteuert erweitert werden, sodass es Partnerunternehmen ermöglicht Unternehmen die eigene Kauf Verlauf und den Kontostatus einsehen. Aus Gründen der Sicherheit befindet sich alle Finanzdaten der Partner in einer geschützten Datenbank auf einem dedizierten Structured Query Language \(SQL\) Server. In diesem Fall den Code im Vordergrund\-End-Anwendung nicht bekannt ist, über die Finanzdaten der Partnerorganisation. Aus diesem Grund müssen sie diese Daten abrufen, von einem anderen Computer im Netzwerk, die hostet \(in diesem Fall\) den Webdienst für die Teiledatenbank \(das Back-End\).  
  
Für diese Daten\-Abruf-Vorgang erfolgreich ist, wird eine Abfolge von Autorisierungs-"Hand\-Schütteln" müssen erfolgen immer zwischen der Web-Anwendung und dem Webdienst für die Teiledatenbank, wie in der folgenden Abbildung dargestellt.  
  
![identitätsdelegierung](media/adfs2_identitydelegationconcept.gif)  
  
Da die ursprüngliche Anforderung an den Webserver selbst gerichtet war, der sich möglicherweise in einer ganz anderen Organisation befindet als der zugreifende Benutzer, entspricht das mit der Anforderung gesendete Sicherheitstoken nicht den Autorisierungskriterien, die für den Zugriff auf andere Computer als den Webserver erforderlich sind. Daher besteht die einzige Möglichkeit, die Anforderung des zugreifenden Benutzers zu erfüllen, in der Bereitstellung eines zwischengeschalteten Verbundservers innerhalb der Ressourcenpartnerorganisation, der ein neues Sicherheitstoken mit den erforderlichen Zugriffsrechten ausstellt.  
  
## <a name="how-does-identity-delegation-work"></a>Wie funktioniert die Identitätsdelegierung?  
Webanwendungen mit Multi-Tier-Anwendungsarchitektur rufen oft Webdienste auf, um gemeinsam genutzte Daten und Funktionen abzurufen. Es ist wichtig für diese Webdienste, die Identität des ursprünglichen Benutzers zu kennen, damit der Dienst Autorisierungsentscheidungen treffen kann und eine Überwachung ermöglicht wird. In diesem Fall im Vordergrund\-End-Webanwendung den Benutzer an den Webdienst als Delegat darstellt. AD FS ermöglicht dieses Szenario, indem Active Directory-Konten als ein Benutzer einer vertrauenden fungieren. Die folgende Abbildung stellt ein solches Szenario mit Identitätsdelegierung dar.  
  
![identitätsdelegierung](media/adfs2_identitydelegationsteps.gif)  
  
1.  Frank versucht wird, um Zugriff auf Teile\-Sortierung Verlauf aus einer Webanwendung in einer anderen Organisation. Sein Clientcomputer anfordert und empfängt ein Token von AD FS für die Vorder-\-enden Teil\-Sortierung der Webanwendung.  
  
2.  Der Clientcomputer sendet eine Anforderung an die Web-Anwendung, einschließlich des in Schritt 1 erhaltenen Tokens als Beleg für die Identität des Clients.  
  
3.  Die Webanwendung muss mit dem Webdienst kommunizieren, um die Transaktion mit dem Client abschließen zu können. Die Webanwendung kontaktiert AD FS, um ein delegierungstoken für die Interaktion mit dem Webdienst zu erhalten. Delegierungstoken sind Sicherheitstoken, die auf einen Delegaten ausgestellt werden, damit dieser als Benutzer auftritt. AD FS gibt ein delegierungstoken mit Ansprüchen bezüglich des Clients, die für den Webdienst vorgesehen.  
  
4.  Die Webanwendung verwendet das Token, das abgerufen wurde, von AD FS in Schritt 3 zum Zugriff auf den Webdienst, der als Client fungiert. Durch Untersuchen des Delegierungstokens kann der Webdienst erkennen, dass die Webanwendung als Client auftritt. Der Webdienst führt seine Autorisierungsrichtlinie aus, protokolliert die Anforderung und gibt die ursprünglich von Frank angeforderten Teileverlaufsdaten an die Webanwendung und somit an Frank aus.  
  
Für Delegaten können AD FS beschränken, die Webdienste für die die Webanwendung ein delegierungstoken anfordern kann. Der Clientcomputer muss nicht über ein Active Directory-Konto verfügen, damit dieser Vorgang möglich ist. Der Webdienst kann also problemlos die Identität des Delegaten ermitteln, der als der Benutzer fungiert. Somit können Webdienste unterschiedliches Verhalten zeigen, je nachdem, ob sie direkt mit dem Clientcomputer kommunizieren oder über einen Delegaten.  
  
## <a name="configuring-ad-fs-for-identity-delegation"></a>Konfigurieren von AD FS für die Identitätsdelegierung  
Sie können die AD FS-Verwaltungs-Snap verwenden\-in AD FS für die identitätsdelegierung konfigurieren, wenn Sie den datenabrufprozess vereinfachen möchten. Nach der Konfiguration, generiert AD FS können neue Sicherheitstoken, die den Autorisierungskontext enthalten, die den Hintergrund\-End-Dienst möglicherweise erfordert, bevor er Zugriff auf die geschützten Daten bereitstellen kann.  
  
AD FS schränkt nicht, welche Benutzeridentitäten angenommen werden können. Nachdem Sie AD FS für die identitätsdelegierung konfigurieren, geschieht Folgendes:  
  
-   Es wird festgelegt, an welche Server die Autorität delegiert werden kann, Token anzufordern, mit denen die Identität von Benutzern angenommen werden kann.  
  
-   Der Identitätskontext für das delegierte Clientkonto und der Server, der als Delegat auftritt, werden festgelegt und separat behandelt.  
  
Sie können die identitätsdelegierung konfigurieren, durch das Hinzufügen der Autorisierungsregeln auf eine relying Party trust im AD FS-Verwaltungs-Snap-\-in. Weitere Informationen hierzu finden Sie unter [Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md).  
  
## <a name="configuring-the-front-end-web-application-for-identity-delegation"></a>Konfigurieren der Vorderseite\-end-Webanwendung für die identitätsdelegierung  
Entwickler haben mehrere Möglichkeiten, mit denen sie entsprechend der Web-Front-Programm\-Anwendung oder ein Dienst zum Umleiten von Delegierungsanfragen an einen AD FS-Computer zu beenden. Weitere Informationen zum Anpassen von Webanwendungen an die Identitätsdelegierung finden Sie im [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
