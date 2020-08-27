---
title: 'AD-Gesamtstruktur Wiederherstellung: Übernahme einer Betriebs Master Rolle'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.openlocfilehash: 7d7b1abfaf7e3ed4f3780ff2d819340ba8fe98c0
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941530"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>AD-Gesamtstruktur Wiederherstellung: Übernahme einer Betriebs Master Rolle

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Mithilfe des folgenden Verfahrens können Sie eine Betriebs Master Rolle (auch als FSMO-Rolle (Flexible Single Master Operations) bezeichnet) übernehmen. Sie können Ntdsutil.exe verwenden, ein Befehlszeilen Tool, das automatisch auf allen Domänen Controllern installiert wird.

## <a name="to-seize-an-operations-master-role"></a>So übernehmen Sie eine Betriebs Master Rolle

1. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

   ```
   ntdsutil
   ```

2. Geben Sie an der Eingabeaufforderung **Ntdsutil:** den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   ```
   roles
   ```

3. Geben Sie den folgenden Befehl an der Eingabeaufforderung für die Verwaltung von **ssmo** ein, und drücken Sie dann die EINGABETASTE:

   ```
   connections
   ```

4. Geben Sie an der Eingabeaufforderung " **Serververbindungen:** " den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   ```
   Connect to server ServerFQDN
   ```

   Dabei ist *ServerFQDN* der voll qualifizierte Domänen Name (Fully Qualified Domain Name, FQDN) dieses Domänen Controllers, z. b.: **Verbinden mit Server nycdc01.example.com**.

   Wenn *ServerFQDN* nicht erfolgreich ist, verwenden Sie den NetBIOS-Namen des Domänen Controllers.

5. Geben Sie an der Eingabeaufforderung " **Serververbindungen:** " den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   ```
   quit
   ```

6. Geben Sie in Abhängigkeit von der Rolle, die Sie übernehmen möchten, den entsprechenden Befehl **in der folgenden** Tabelle ein, und drücken Sie dann die EINGABETASTE.

|Role|Anmeldeinformationen|Get-Help|
|----------|-----------------|-------------|
|Domänen Namen Master|Organisationsadministratoren|**Benennungs Master**|
|Schema Master|Schema-Admins|**Schema Master übernehmen**|
|Infrastruktur Master **Hinweis:**  nachdem Sie die Infrastruktur Master Rolle übernommen haben, erhalten Sie möglicherweise später eine Fehlermeldung, wenn Sie adprep/rodcprep. ausführen müssen. Weitere Informationen finden Sie im KB-Artikel [949257](https://support.microsoft.com/kb/949257).|Domänenadministratoren|**Infrastruktur Master übernehmen**|
|PDC-Emulator-Master|Domänenadministratoren|**PDC übernehmen**|
|-RID-Master|Domänenadministratoren|**RID-Master übernehmen**|

Nachdem Sie die Anforderung bestätigt haben, werden Active Directory oder AD DS versucht, die Rolle zu übertragen. Wenn die Übertragung fehlschlägt, werden einige Fehlerinformationen angezeigt, und Active Directory oder AD DS wird mit der Beschlagnahme fortgesetzt. Nachdem der Vorgang durchgeführt wurde, wird eine Liste der Rollen und der LDAP-Name (Lightweight Directory Access Protocol) des Servers angezeigt, der derzeit die jeweilige Rolle innehat. Sie können **netdom query fsmo** auch an einer Eingabeaufforderung mit erhöhten Rechten ausführen, um die aktuellen Rollen Inhaber zu überprüfen.

> [!NOTE]
> Wenn dieser Computer vor dem Auftreten des Fehlers kein RID-Master war und Sie versuchen, die RID-Master Rolle zu übernehmen, versucht der Computer, eine Synchronisierung mit einem Replikations Partner durchführen, bevor diese Rolle akzeptiert Da dieser Schritt jedoch bei der Isolierung des Computers durchgeführt wird, ist die Synchronisierung mit einem Partner nicht erfolgreich. Daher wird ein Dialogfeld angezeigt, in dem Sie gefragt werden, ob der Vorgang fortgesetzt werden soll, obwohl der Computer nicht mit einem Partner synchronisiert werden kann. Klicken Sie auf **Ja**.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
