---
ms.assetid: 19feca0e-a6d0-4d27-93b0-cb44f8c26484
title: Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 00a8eec9936b03fffa9718bc31bfb05e733d1022
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941100"
---
# <a name="delegating-administration-of-account-ous-and-resource-ous"></a>Delegieren der Verwaltung von Konten- und Ressourcenorganisationseinheiten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konto Organisationseinheiten (OUs) enthalten Benutzer-, Gruppen-und Computer Objekte. Die Ressourcen Organisationseinheiten enthalten Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstruktur Besitzer ist dafür verantwortlich, eine OE-Struktur zu erstellen, um diese Objekte und Ressourcen zu verwalten und die Steuerung dieser Struktur an den Besitzer der Organisationseinheit zu delegieren.

## <a name="delegating-administration-of-account-ous"></a>Delegieren der Verwaltung von Account OUs
Delegieren Sie eine Konto-OE-Struktur an Daten Administratoren, wenn Sie Benutzer-, Gruppen-und Computer Objekte erstellen und ändern müssen. Die Konto-OE-Struktur ist eine Teilstruktur von Organisationseinheiten für jeden Kontotyp, der unabhängig kontrolliert werden muss. Beispielsweise kann der Besitzer der Organisationseinheit bestimmte Kontrolle an verschiedene Daten Administratoren über die untergeordneten Organisationseinheiten in einer Konto-Organisationseinheit für Benutzer, Computer, Gruppen und Dienst Konten delegieren.

Die folgende Abbildung zeigt ein Beispiel für eine Konto-OE-Struktur.

![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/66d38fbe-e8eb-42d7-abab-9526243bf6d9.gif)

In der folgenden Tabelle sind die möglichen untergeordneten Organisationseinheiten aufgeführt und beschrieben, die Sie in einer Konto-OE-Struktur erstellen können.

|OU|Zweck|
|------|-----------|
|Benutzer|Enthält Benutzerkonten für nicht administrative Mitarbeiter.|
|Dienstkonten|Einige Dienste, die Zugriff auf Netzwerkressourcen benötigen, werden als Benutzerkonten ausgeführt. Diese Organisationseinheit wird erstellt, um Dienst Benutzerkonten von den Benutzerkonten in der Organisationseinheit Benutzer zu trennen. Wenn Sie die verschiedenen Arten von Benutzerkonten in separaten Organisationseinheiten platzieren, können Sie Sie auch entsprechend Ihren speziellen administrativen Anforderungen verwalten.|
|Computers|Enthält Konten für Computer, die keine Domänen Controller sind.|
|Gruppen|Enthält Gruppen aller Typen außer administrativen Gruppen, die separat verwaltet werden.|
|Administratoren|Enthält Benutzer-und Gruppenkonten für Daten Administratoren in der Organisations-OE-Struktur, damit diese separat von regulären Benutzern verwaltet werden können. Aktivieren Sie die Überwachung für diese Organisationseinheit, damit Sie Änderungen an Administratoren und Gruppen nachverfolgen können.|

In der folgenden Abbildung ist ein Beispiel für einen administrativen Gruppen Entwurf für eine Konto-OE-Struktur dargestellt.

![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/be2cd2d2-6956-429c-a53a-369e6fe40b2b.gif)

Gruppen, die die untergeordneten Organisationseinheiten verwalten, erhalten Vollzugriff nur über die spezifische Klasse von Objekten, für deren Verwaltung Sie zuständig sind.

Die Typen von Gruppen, die Sie verwenden, um die Steuerung innerhalb einer Organisations Einheits Struktur zu delegieren, basieren darauf, wo sich die Konten befinden, in Bezug auf die zu verwaltende OE-Struktur. Wenn die Administrator Benutzerkonten und die OE-Struktur alle innerhalb einer einzelnen Domäne vorhanden sind, müssen die Gruppen, die Sie für die Delegierung verwenden, globale Gruppen sein. Wenn Ihre Organisation über eine Abteilung verfügt, die ihre eigenen Benutzerkonten verwaltet und in mehr als einer geografischen Region vorhanden ist, verfügen Sie möglicherweise über eine Gruppe von Daten Administratoren, die für die Verwaltung der Konto Organisationseinheiten in mehr als einer Domäne verantwortlich sind. Wenn die Konten der Daten Administratoren alle in einer einzelnen Domäne vorhanden sind und Sie über OE-Strukturen in mehreren Domänen verfügen, für die Sie die Steuerung delegieren müssen, nehmen Sie diese administrativen Konten als Mitglieder globaler Gruppen an, und delegieren Sie die Kontrolle über die Organisationseinheiten Strukturen in jeder Domäne an diese globalen Gruppen. Wenn die Daten Administratoren, an die Sie die Steuerung einer OE-Struktur delegieren, von mehreren Domänen stammen, müssen Sie eine universelle Gruppe verwenden. Universelle Gruppen können Benutzer aus unterschiedlichen Domänen enthalten und können daher zum Delegieren der Steuerung in mehreren Domänen verwendet werden.

## <a name="delegating-administration-of-resource-ous"></a>Delegieren der Verwaltung von Ressourcen-OUs
Ressourcen-OUs werden verwendet, um den Zugriff auf Ressourcen zu verwalten. Der Besitzer der Ressourcen-Organisationseinheit erstellt Computer Konten für Server, die der Domäne hinzugefügt werden, die Ressourcen wie Dateifreigaben, Datenbanken und Drucker enthält. Der Besitzer der Ressourcen-Organisationseinheit erstellt außerdem Gruppen zum Steuern des Zugriffs auf diese Ressourcen.

Die folgende Abbildung zeigt die beiden möglichen Standorte für die Ressourcen-OE.

![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/6667a5ce-34d6-48a9-9974-b823ba70e2af.gif)

Die Ressourcen-Organisationseinheit befindet sich unter dem Domänen Stammverzeichnis oder als untergeordnete OE der entsprechenden Konto-Organisationseinheit in der Hierarchie der Organisationseinheit. Die Ressourcen-OUs verfügen über keine standardmäßigen untergeordneten Organisationseinheiten. Computer und Gruppen werden direkt in der Ressourcen-Organisationseinheit platziert.

Der Besitzer der Ressourcen-Organisationseinheit besitzt die Objekte in der Organisationseinheit, ist aber nicht Besitzer des ou-Containers. Ressourcen-OU-Besitzer verwalten nur Computer-und Gruppen Objekte; Sie können keine anderen Klassen von Objekten innerhalb der Organisationseinheit erstellen, und Sie können keine untergeordneten Organisationseinheiten erstellen.

> [!NOTE]
> Der Ersteller oder Besitzer eines Objekts kann die Zugriffs Steuerungs Liste (Access Control List, ACL) für das Objekt unabhängig von den Berechtigungen festlegen, die vom übergeordneten Container geerbt werden. Wenn der Besitzer einer Ressourcen-Organisationseinheit die ACL für eine Organisationseinheit zurücksetzen kann, kann dieser Besitzer eine beliebige Objektklasse in der Organisationseinheit erstellen, einschließlich der Benutzer. Aus diesem Grund ist es nicht zulässig, Organisationseinheiten der Ressourcen-OE Organisationseinheiten zu erstellen.

Erstellen Sie für jede Ressourcen-Organisationseinheit in der Domäne eine globale Gruppe, die die Daten Administratoren darstellt, die für die Verwaltung des Inhalts der Organisationseinheit zuständig sind. Diese Gruppe verfügt über vollständige Kontrolle über die Gruppen-und Computer Objekte in der Organisationseinheit, jedoch nicht über den OU-Container selbst.

Die folgende Abbildung zeigt den Entwurf der administrativen Gruppe für eine Ressourcen-Organisationseinheit.

![Delegieren der Verwaltung](media/Delegating-Administration-of-Account-OUs-and-Resource-OUs/8a3f7714-a3bf-43f7-b999-6070543248b0.gif)

Durch das Platzieren der Computer Konten in einer Ressourcen-Organisationseinheit erhält der OU-Besitzer die Kontrolle über die Konto Objekte, aber der OE-Besitzer wird nicht zu einem Administrator der Computer. In einer Active Directory Domäne ist die Gruppe Domänen-Admins standardmäßig in der Gruppe lokale Administratoren auf allen Computern abgelegt. Das heißt, dass Dienst Administratoren die Kontrolle über diese Computer haben. Wenn Besitzer der Organisationseinheit die administrative Kontrolle über die Computer in Ihrem Organisationseinheiten Element benötigen, kann der Gesamtstruktur Besitzer eingeschränkte Gruppen Gruppenrichtlinie anwenden, um den Besitzer der Ressourcen-Organisationseinheit zu einem Mitglied der Gruppe "Administratoren" auf den Computern in dieser Organisationseinheit zu machen.



