---
ms.assetid: 19feca0e-a6d0-4d27-93b0-cb44f8c26484
title: Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 56e69bffdf8ecc0f37f9f5159ae6bce7fcdc49f8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-of-account-ous-and-resource-ous"></a>Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Konto-Organisationseinheiten (OUs) werden Benutzer, Gruppen und Computer Objekte enthalten. Ressourcenorganisationseinheiten enthalten die Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstrukturbesitzer ist für das Erstellen einer OE-Struktur, um diese Objekte und Ressourcen zu verwalten und Delegieren der Steuerung dieser Struktur der Organisationseinheit Besitzer verantwortlich.  
  
## <a name="delegating-administration-of-account-ous"></a>Delegieren der Verwaltung von Konto-OEs  
Weisen Sie ein Konto-OE-Struktur den Datenadministratoren, wenn eine Benutzer-, Gruppen- und Computer Objekte erstellen und ändern. Das Konto-OE-Struktur ist eine Unterstruktur der Organisationseinheiten für die einzelnen Kontotypen, die unabhängig voneinander gesteuert werden muss. Der Besitzer kann z. B. bestimmte Steuerelemente für verschiedene Datenadministratoren über untergeordnete Organisationseinheiten in einem Konto Organisationseinheit für Benutzer, Computer, Gruppen und Dienstkonten delegieren.  
  
Die folgende Abbildung zeigt ein Beispiel für ein Konto-OE-Struktur.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/66d38fbe-e8eb-42d7-abab-9526243bf6d9.gif)  
  
In der folgende Tabelle aufgelistet und beschrieben von den möglichen untergeordneten Organisationseinheiten, die Sie in einem Konto-OE-Struktur erstellen können.  
  
|ORGANISATIONSEINHEIT|Zweck|  
|------|-----------|  
|Benutzer|Enthält die Benutzerkonten für nicht administrative Mitarbeiter.|  
|Dienstkonten|Einige Dienste, die Zugriff auf Netzwerkressourcen benötigen werden als Benutzerkonten ausführen. Diese Organisationseinheit wird separate Service-Benutzerkonten aus der Benutzerkonten, die in der Organisationseinheit dem Benutzer erstellt. Ermöglicht außerdem die verschiedenen Typen von Benutzerkonten in separate Organisationseinheiten platzieren Sie sie entsprechend ihren spezifischen administrativen Anforderungen zu verwalten.|  
|Computer|Konten für Computer als Domänencontroller enthält.|  
|Gruppen|Enthält eine Gruppe aller Typen mit Ausnahme von administrativen Gruppen, die separat verwaltet werden.|  
|"Administratoren"|Enthält Benutzer- und Gruppenkonten für Datenadministratoren im Konto-OE-Struktur aus regulären Benutzern separat verwaltet werden können. Aktivieren Sie die Überwachung für diese Organisationseinheit, damit Sie Änderungen an Administratoren und Gruppen nachverfolgen können.|  
  
Die folgende Abbildung zeigt ein Beispiel für eine verwaltungsgruppendesign für ein Konto-OE-Struktur.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/be2cd2d2-6956-429c-a53a-369e6fe40b2b.gif)  
  
Gruppen, die die untergeordneten Organisationseinheiten verwalten sind nur über bestimmte Klasse von Objekten Vollzugriff für die Verwaltung zuständig sind.  
  
Die Arten von Gruppen, die Sie verwenden, um innerhalb einer OE-Struktur delegieren basieren auf, wo sich die Konten relativ zu der OE-Struktur befinden, die verwaltet werden. Wenn die Admin-Benutzerkonten und Struktur der Organisationseinheiten innerhalb einer einzelnen Domäne vorhanden sind, müssen die Gruppen, die Sie erstellen, um für die Delegierung verwenden globale Gruppen sein. Wenn Ihre Organisation eine Abteilung, die einen eigenen Benutzerkonten verwaltet und in mehr als eine geografische Region vorhanden ist verfügt, verfügen Sie möglicherweise eine Gruppe von Datenadministratoren, die für die Verwaltung von Konto-OEs in mehreren Domänen zuständig sind. Wenn die Konten der alle Datenadministratoren vorhanden, in einer einzelnen Domäne sind und OU-Strukturen in mehreren Domänen delegiert werden müssen, stellen Sie diese Konten Mitglieder globaler Gruppen und Delegieren Sie der Verwaltung der OU-Strukturen in jeder Domäne an diesen globalen Gruppen. Wenn die Daten Administratorenkonten, die Sie eine OE-Struktur delegieren, aus mehreren Domänen stammen, müssen Sie eine universelle Gruppe verwenden. Universelle Gruppen können Benutzer aus anderen Domänen enthalten, und sie können daher verwendet werden, um in mehreren Domänen delegieren.  
  
## <a name="delegating-administration-of-resource-ous"></a>Delegieren der Verwaltung von Ressourcen-OUs  
Ressourcenorganisationseinheiten werden verwendet, um den Zugriff auf Ressourcen zu verwalten. Der Besitzer der Ressource Organisationseinheit erstellt Computerkonten für Server, die der Domäne angehören, die Ressourcen wie z. B. Dateifreigaben, Datenbanken und Drucker enthalten. Der Besitzer der Ressource Organisationseinheit erstellt auch Gruppen, um den Zugriff auf diese Ressourcen zu steuern.  
  
Die folgende Abbildung zeigt die zwei möglichen Positionen für die OU-Ressource.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/6667a5ce-34d6-48a9-9974-b823ba70e2af.gif)  
  
Die Ressource Organisationseinheit kann sich unter dem Domänenstamm oder als eine untergeordnete Organisationseinheit des entsprechenden Kontos Organisationseinheit in der Hierarchie der Organisationseinheiten administrative befinden. Ressourcenorganisationseinheiten müssen keine standardmäßigen untergeordnete Organisationseinheiten. Computer und Gruppen werden direkt in der Ressourcen-OU platziert.  
  
Besitzer der Ressource gehören die Objekte in der Organisationseinheit, aber es ist nicht im Besitz des OU-Containers selbst. Organisationseinheit Ressourcenbesitzer verwalten nur Computer- und Gruppenobjekten. Sie können nicht andere Klassen von Objekten in einer Organisationseinheit erstellen, und sie können keine untergeordneten Organisationseinheiten erstellen.  
  
> [!NOTE]  
> Der Ersteller oder Besitzer eines Objekts hat die Möglichkeit zum Festlegen der Zugriffssteuerungsliste (ACL) für das Objekt unabhängig von den Berechtigungen, die vom übergeordneten Container geerbt werden. Wenn Sie eine Organisationseinheit Ressourcenbesitzer die ACL für eine Organisationseinheit zurückgesetzt werden kann, kann die Besitzer eine Klasse des Objekts in der Organisationseinheit, einschließlich der Benutzer erstellen. Aus diesem Grund sind die Ressourcenbesitzer Organisationseinheit nicht zulässig, Organisationseinheiten zu erstellen.  
  
Erstellen Sie für jede Ressource Organisationseinheit in der Domäne eine globale Gruppe, die Datenadministratoren darstellen, die für die Verwaltung der Inhalte der Organisationseinheit zuständig sind. Diese Gruppe über Vollzugriff auf die Gruppe und Computerobjekte in der Organisationseinheit, jedoch nicht über die OU-Container selbst verfügt.  
  
Die folgende Abbildung zeigt den administrativen Gruppenentwurf für eine Ressource Organisationseinheit.  
  
![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/8a3f7714-a3bf-43f7-b999-6070543248b0.gif)  
  
Platzieren die Computerkonten in einer Organisationseinheit-Ressource verfügt der Organisationseinheit Besitzer Kontrolle über die Kontoobjekte jedoch nicht der Besitzer ein Administrator den Computer. In einer Active Directory-Domäne ist, der Gruppe "Domänen-Admins" in der lokalen Administratorengruppe auf allen Computern in der Standardeinstellung platziert. Das heißt, haben Dienstadministratoren Kontrolle über diese Computer. Wenn Organisationseinheit Ressourcenbesitzer administrativen Kontrolle über die Computer in ihrer Organisationseinheiten benötigen, kann der Gesamtstrukturbesitzer eine Richtlinie für eingeschränkte Gruppen Gruppe um Besitzer der Ressource ein Mitglied der Gruppe "Administratoren" auf die Computer in einer Organisationseinheit anwenden.  
  


