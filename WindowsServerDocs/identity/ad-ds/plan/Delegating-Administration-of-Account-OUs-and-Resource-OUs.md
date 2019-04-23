---
ms.assetid: 19feca0e-a6d0-4d27-93b0-cb44f8c26484
title: Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 70900b44de85774e8e595f9691885d67682fa753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834261"
---
# <a name="delegating-administration-of-account-ous-and-resource-ous"></a>Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konto-Organisationseinheiten (OUs) werden die Benutzer-, Gruppen- und Computer-Objekte enthalten. Ressourcenorganisationseinheiten enthalten Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstrukturbesitzer ist verantwortlich für das Erstellen einer OE-Struktur, um diese Objekte und Ressourcen zu verwalten und Delegieren der Steuerung von dieser Struktur der Organisationseinheit Besitzer.  
  
## <a name="delegating-administration-of-account-ous"></a>Delegieren der Verwaltung der Konto-OEs  
Delegieren Sie ein Konto-OE-Struktur, um Data-Administratoren, wenn eine Benutzer-, Gruppen- und Computer-Objekte erstellen und ändern. Das Konto-OE-Struktur ist eine Unterstruktur von Organisationseinheiten für jeden Kontotyp, die unabhängig voneinander kontrolliert werden muss. Beispielsweise kann der OE-Besitzer über untergeordnete Organisationseinheiten in einem Konto Organisationseinheit für Benutzer, Computer, Gruppen und Dienstkonten bestimmtes Steuerelement an verschiedene Datenadministratoren delegieren.  
  
Die folgende Abbildung zeigt ein Beispiel für ein Konto-OE-Struktur.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/66d38fbe-e8eb-42d7-abab-9526243bf6d9.gif)  
  
Die folgende Tabelle enthält und beschreibt die möglichen untergeordneten Organisationseinheiten, die Sie in einem Konto-OE-Struktur erstellen können.  
  
|OU|Zweck|  
|------|-----------|  
|Benutzer|Benutzerkonten enthält für nicht administrative Mitarbeiter.|  
|Dienstkonten|Einige Dienste, die Zugriff auf Netzwerkressourcen erforderlich ist, die als Benutzerkonten ausführen werden. Diese Organisationseinheit wird von den Benutzerkonten in die Benutzer-Organisationseinheit enthaltenen, gesonderte Dienstkonten für Benutzer erstellt. Ermöglicht außerdem die verschiedenen Typen von Benutzerkonten in separate Organisationseinheiten platzieren Sie sie entsprechend ihren spezifischen administrativen Anforderungen verwalten.|  
|Computer|Enthält Konten, die für Computer als Domänencontroller.|  
|Gruppen|Enthält Gruppen aller Typen mit Ausnahme von administrativen Gruppen, die separat verwaltet werden.|  
|Administratoren|Enthält von Benutzer- und Gruppenkonten für Datenadministratoren in die Konto-OE-Struktur um reguläre Benutzer separat verwaltet werden können. Aktivieren Sie die Überwachung für diese Organisationseinheit, damit Sie Änderungen an Administratoren und Gruppen nachverfolgen können.|  
  
Die folgende Abbildung zeigt ein Beispiel für eine administrative Gruppenentwurf für ein Konto-OE-Struktur.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/be2cd2d2-6956-429c-a53a-369e6fe40b2b.gif)  
  
Gruppen, die die untergeordneten Organisationseinheiten verwalten erhalten die volle Kontrolle über die spezifische Klasse von Objekten nur, dass sie für die Verwaltung zuständig sind.  
  
Die Typen von Gruppen, mit denen Sie eine OE-Struktur delegieren hängen davon ab, wo sich die Konten relativ zu der OE-Struktur befinden, die verwaltet werden. Wenn die Admin-Benutzerkonten und Struktur der Organisationseinheiten innerhalb einer einzelnen Domäne vorhanden sind, müssen die Gruppen, die Sie erstellen, um für die Delegierung zu verwenden, globale Gruppen sein. Wenn Ihre Organisation eine Abteilung, die eine eigene Benutzerkonten verwaltet und in mehreren geografischen Regionen vorhanden ist verfügt, müssen Sie eine Gruppe von Datenadministratoren möglicherweise, die für die Verwaltung von Konto-OEs in mehreren Domänen zuständig sind. Wenn die Konten der Datenadministratoren alle, die in einer einzelnen Domäne vorhanden sind, und man OE-Strukturen in mehreren Domänen, die auf die Sie delegieren möchten, stellen Sie diese Administratorkonten Mitglieder globaler Gruppen und Delegieren Sie der Verwaltung der OE-Strukturen in den einzelnen Domäne, die diesen globalen Gruppen. Wenn die Daten Administratorkonten, die zu denen Sie eine OU-Struktur delegieren aus mehreren Domänen stammen, müssen Sie eine universelle Gruppe verwenden. Universelle Gruppen können Benutzer aus anderen Domänen enthalten, und sie können aus diesem Grund verwendet werden, in mehreren Domänen delegiert.  
  
## <a name="delegating-administration-of-resource-ous"></a>Delegieren der Verwaltung von Ressourcen Organisationseinheiten  
Ressourcenorganisationseinheiten werden verwendet, um den Zugriff auf Ressourcen zu verwalten. Der Besitzer der Ressource Organisationseinheit erstellt die Computerkonten für Server, die der Domäne beigetreten sind, die Ressourcen wie z. B. Dateifreigaben, Datenbanken und Drucker enthalten. Der Besitzer der Ressource Organisationseinheit erstellt außerdem Gruppen, um den Zugriff auf diese Ressourcen zu steuern.  
  
Die folgende Abbildung zeigt die beiden Standorte für die Ressource Organisationseinheit.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/6667a5ce-34d6-48a9-9974-b823ba70e2af.gif)  
  
Die Ressource kann Organisationseinheit befindet, unter dem Domänenstamm oder als eine untergeordnete Organisationseinheit des entsprechenden Kontos Organisationseinheit in der Hierarchie der Organisationseinheiten administrative sein. Ressourcenorganisationseinheiten müssen keine standardanordnung von untergeordneten Organisationseinheiten. Computer und Gruppen werden direkt in der OE-Ressource platziert werden.  
  
Der Besitzer der Ressource Organisationseinheit besitzt die Objekte in der Organisationseinheit, aber nicht für die OU-Container selbst zuständig. Organisationseinheit Ressourcenbesitzer verwalten nur die Computer- und Gruppenobjekten; Sie können andere Klassen von Objekten in der Organisationseinheit können nicht erstellt, und sie können keine untergeordneten Organisationseinheiten erstellen.  
  
> [!NOTE]  
> Der Ersteller oder Besitzer eines Objekts hat sich die Möglichkeit, legen Sie die Zugriffssteuerungsliste (ACL) für das Objekt unabhängig von den Berechtigungen, die vom übergeordneten Container geerbt werden. Wenn ein Ressourcenbesitzer-Organisationseinheit die ACL für eine Organisationseinheit zurücksetzen kann, kann dieser Besitzer jede Klasse des Objekts in der Organisationseinheit, einschließlich der Benutzer erstellen. Aus diesem Grund sind die Organisationseinheit Ressourcenbesitzer nicht zulässig, um Organisationseinheiten zu erstellen.  
  
Erstellen Sie für jede Organisationseinheit in der Domäne der Ressource die eine globale Gruppe der Datenadministratoren darstellt, die für die Verwaltung des Inhalts der Organisationseinheit zuständig sind. Diese Gruppe hat vollständige Kontrolle über die Gruppen- und Computerobjekte in der Organisationseinheit, jedoch nicht über die OU-Container selbst.  
  
Die folgende Abbildung zeigt die verwaltungsgruppendesign für eine Ressource Organisationseinheit.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/8a3f7714-a3bf-43f7-b999-6070543248b0.gif)  
  
Platzieren die Computerkonten in eine Ressource Organisationseinheit kann die Organisationseinheit Besitzer steuern die Kontoobjekte aber macht nicht dem Besitzer der Organisationseinheit ein Administrator den Computer. In einer Active Directory-Domäne ist, die Gruppe "Domänenadministratoren" in der Standardeinstellung in der lokalen Administratorgruppe auf allen Computern platziert. Dienstadministratoren haben, also Kontrolle über diese Computer. Wenn OE Ressourcenbesitzer administrativen Kontrolle über die Computer in ihrer Organisationseinheiten benötigen, kann der Gesamtstrukturbesitzer eine eingeschränkte Gruppen Gruppenrichtlinie OU-Besitzer der Ressource Mitglied der Gruppe "Administratoren" auf den Computern in dieser Organisationseinheit stellen anwenden.  
  


