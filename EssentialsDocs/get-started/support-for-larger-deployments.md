---
title: Unterstützung für größere Bereitstellungen
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d98ab8b203bc73da4129d63b5a2b7518742a3667
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181646"
---
# <a name="support-for-larger-deployments"></a>Unterstützung für größere Bereitstellungen

>Gilt für: Windows Server 2016 Essentials

> [!IMPORTANT]
> Die in diesem Thema beschriebenen Funktionen funktionieren nur unter Windows Server 2016 mit aktivierter Essentials-Benutzerrolle und nicht mit der Windows Server 2016 Essentials-SKU.


Windows Server Essentials unterstützt jetzt größere bereit Stellungen mit folgenden Aktionen:

- mehrere Domänen
- mehrere Domänen Controller
- Möglichkeit zum Angeben eines bestimmten Domänen Controllers
- Unterstützung für bis zu 500 Benutzer und 500 Geräte

## <a name="support-for-multiple-domains"></a>Unterstützung mehrerer Domänen

Windows Server 2012 R2 Essentials unterstützt nur eine Domäne pro Server, was erforderlich ist, und der Essentials-Server muss der Stamm der Gesamtstruktur sein. Obwohl eine Domäne und Gesamtstruktur weiterhin erforderlich sind, kann die Rolle Windows Server 2016 Essentials-Benutzer jetzt unter Windows Server 2016 Standard oder Datacenter bereitgestellt werden, um mehrere Domänen zu unterstützen.

## <a name="support-for-multiple-domain-controllers"></a>Unterstützung für mehrere Domänen Controller

 Windows Server Essentials 2012 R2 blockiert alle Dienste, die Azure Active Directory nutzen, wie z. b. Office 365, bei denen mehr als ein Domänen Controller bereitgestellt wird. Der Grund hierfür ist, dass die Konto-und Kenn Wort Synchronisierung zwischen den lokalen Domänen Controllern und Azure Active Directory zu Konto Anmelde Informationen mit Kenn Wörtern führen kann, die nicht synchron sind. Diese Einschränkung wurde in Windows Server 2016 Essentials entfernt.

## <a name="ability-to-specify-a-designated-domain-controller"></a>Möglichkeit zum Angeben eines bestimmten Domänen Controllers

Sie können jetzt einen designierten Domänen Controller auswählen, der die Abrufzeiten für Active Directory Domänen Objekte verbessern und die Synchronisierung der Konto Änderung auf anderen Domänen Controllern in der Domäne koordiniert.

Der standardmäßig festgelegte Domänen Controller ist derselbe Server, auf dem die Server Rolle "Windows Server Essentials-Server" ausgeführt wird. Wenn dieser Server ein Mitglieds Server ist, d. h. er ist kein Domänen Controller, wird der standardmäßig festgelegte Domänen Controller automatisch basierend auf dem Testen bestimmt, welcher Domänen Controller in der Domäne über die niedrigste Netzwerk Latenz für den Server verfügt, auf dem die Server Rolle "Windows Server" ausgeführt wird. Wenn Sie manuell ändern möchten, welcher Server der vorgesehene Domänen Controller ist, können Sie dies unter **Einstellungen** im **Windows Server Essentials-Dashboard** tun, wie unten gezeigt.

![Ein Screenshot, der die Einstellungen-Systemsteuerung im Vordergrund und das Windows Server Essentials-Dashboard im Hintergrund anzeigt. Die Seite für den designierten Domänen Controller der Einstellungs Systemsteuerung ist derzeit ausgewählt.](media/larger-deployments-1.PNG)

## <a name="support-for-500-users-and-500-devices"></a>Unterstützung für 500-Benutzer und 500-Geräte
-------------------------------------

Die maximale Anzahl unterstützter Benutzer und Geräte in Windows Server 2012 R2 Essentials beträgt 25 bzw. 50. Mit der Einführung der Windows Server Essentials-Server Rolle wurde dieser Grenzwert auf 100 Benutzer und 200 Geräte angehoben.

Windows Server 2016 Essentials unterstützt 500-Benutzer und 500-Geräte. Dies ermöglicht ein Update der Steuerelemente für das Anbieter Framework und die Objektliste, sodass Sie große Benutzer-und Geräte Objektlisten Zwischenspeichern und schnell darstellen. Außerdem wurde eine Such-und Filterfunktion hinzugefügt, mit der Sie den Benutzer oder das Gerät, nach dem Sie suchen, schnell finden können (siehe Abbildung 5-2). Die Such-und Filterfunktionen finden Sie im **Windows Server Essentials-Dashboard**, in **Remote Webzugriff**und in den Windows-und Windows Phone Speichern von **My Server** -Anwendungen.

![Ein Screenshot, der die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards für die Suche nach der Zeichenfolge "d5c" anzeigt. Die Ergebnisse dieser Suche enthalten zwei Dateien und Ordner und zwei Benutzer.](media/larger-deployments-2.PNG)

Ein Screenshot, der die Verwendung der Suchfunktion des Windows Server Essentials-Dashboards für die Suche nach der Zeichenfolge "d5c" anzeigt. Die Ergebnisse dieser Suche enthalten zwei Dateien und Ordner und zwei Benutzer.

> [!NOTE]
> Obwohl die unterstützte Benutzer-und Geräte Beschränkung für die Windows Server Essentials-Server Rolle gestiegen ist, bleibt das unterstützte Limit für die Client Sicherungskopie bei 75.

<a name="see-also"></a>Weitere Informationen
--------
[Erste Schritte in Windows Server Essentials](get-started.md)