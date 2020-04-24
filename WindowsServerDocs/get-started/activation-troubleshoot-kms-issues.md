---
title: 'KMS-Aktivierung: bekannte Probleme'
description: Beschreibt häufige Probleme, die während des KMS-Aktivierungsvorgangs auftreten können, und bietet Lösungen und Anleitungen.
ms.topic: article
ms.date: 10/3/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 3446ad0954510d8c96e9a2d361f24c90d325b782
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826253"
---
# <a name="kms-activation-known-issues"></a>KMS-Aktivierung: bekannte Probleme

In diesem Artikel werden häufige Fragen und Probleme beschrieben, die bei der Aktivierung mittels Schlüsselverwaltungsdienst (KMS) auftreten können, sowie Anleitungen zur Behebung der Probleme.

> [!NOTE]
> Wenn du vermutest, dass dein Problem mit dem DNS in Zusammenhang steht, findest du Informationen hierzu unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).

## <a name="should-i-back-up-kms-host-information"></a>Sollte ich die KMS-Hostinformationen sichern?

Eine Sicherung ist für KMS-Hosts nicht erforderlich. Wenn du jedoch ein Tool verwendest, um Ereignisprotokolle regelmäßig zu bereinigen, kann der Aktivierungsverlauf, der in den Protokollen gespeichert ist, verloren gehen. Wenn du das Ereignisprotokoll verwendest, um KMS-Aktivierungen zu verfolgen oder zu dokumentieren, exportierst du das Ereignisprotokoll des Schlüsselverwaltungsdiensts in regelmäßigen Abständen aus dem Protokolleordner „Anwendungen und Dienste“ in der Ereignisanzeige.

Wenn du System Center Operations Manager verwendest, speichert die System Center Data Warehouse-Datenbank Ereignisprotokolldaten für die Berichterstellung, weshalb du die Ereignisprotokolle nicht separat sichern musst.

## <a name="is-the-kms-client-computer-activated"></a>Ist der KMS-Clientcomputer aktiviert?

Öffne auf dem KMS-Clientcomputer die **Systemsteuerung**, und suche nach der Meldung **Windows ist aktiviert**. Führe alternativ „Slmgr.vbs“ aus, und verwende die Befehlszeilenoption **/dli**.

## <a name="the-kms-client-computer-does-not-activate"></a>Der KMS-Clientcomputer wird nicht aktiviert.

Überprüfe, ob der KMS-Aktivierungsschwellenwert erreicht wird. Führe auf dem KMS-Hostcomputer „Slmgr.vbs“ aus, und verwende die Befehlszeilenoption **/dli**, um die aktuelle Anzahl des Hosts zu ermitteln. Windows 7-Clientcomputer können erst aktiviert werden, wenn der KMS-Host eine Anzahl von 25 besitzt. Für die Aktivierung von Windows Server 2008 R2-KMS-Clients ist eine KMS-Anzahl von 5 erforderlich. Weitere Informationen zur KMS-Anforderungen findest du im [Bereitstellungshandbuch zur Volumenaktivierung](https://go.microsoft.com/fwlink/?linkid=155926). 

Suche auf dem KMS-Clientcomputer im Anwendungsereignisprotokoll nach der Ereignis-ID 12289. Überprüfe dieses Ereignis auf die folgenden Informationen:

- Ist der Ergebniscode **0**? Alles andere ist ein Fehler.
- Ist der KMS-Hostname im Ereignis richtig?
- Ist der KMS-Port richtig?
- Ist der KMS-Host zugänglich?
- Wenn auf dem Client eine andere als die Microsoft-Firewall ausgeführt wird, muss dann der ausgehende Port konfiguriert werden?

Suche auf dem KMS-Clientcomputer im KMS-Ereignisprotokoll nach der Ereignis-ID 12290. Überprüfe dieses Ereignis auf die folgenden Informationen:

- Hat der KMS-Host eine Anforderung von dem Clientcomputer protokolliert? Vergewissere dich, dass der Name des KMS-Clientcomputers aufgeführt ist. Vergewissere dich, dass Client und KMS-Host kommunizieren können. Hat der Client die Antwort erhalten?
- Wenn vom KMS-Client kein Ereignis protokolliert wird, hat die Anforderung den KMS-Host nicht erreicht, oder der KMS-Host konnte sie nicht verarbeiten. Stelle sicher, dass Router keinen Datenverkehr über den TCP-Port 1688 blockieren (wenn der Standardport verwendet wird) und dass zustandsbehafteter Datenverkehr an den KMS-Client zulässig ist.

## <a name="what-does-this-error-code-mean"></a>Was bedeutet dieser Fehlercode?

Mit Ausnahme von KMS-Ereignissen mit der Ereignis-ID 12290 protokolliert Windows alle Aktivierungsereignisse im Anwendungsereignisprotokoll unter dem Ereignisanbieternamen „Microsoft-Windows-Security-SPP“. Windows protokolliert KMS-Ereignisse im Schlüsselverwaltungsdienst-Protokoll im Ordner „Anwendungen und Dienste“. IT-Spezialisten können „Slui.exe“ ausführen, um eine Beschreibung der meisten aktivierungsbezogenen Fehlercodes anzuzeigen. Die allgemeine Syntax für diesen Befehl lautet wie folgt:

```cmd
slui.exe 0x2a ErrorCode
```

Wenn z. B. die Ereignis-ID 12293 den Fehlercode „0x8007267C“ enthält, kannst du eine Beschreibung dieses Fehlers anzeigen, indem du den folgenden Befehl ausführst:

```cmd
slui.exe 0x2a 0x8007267C
```

Weitere Informationen zu bestimmten Fehlercodes und deren Behebung findest du unter [Auflösen von gängigen Aktivierungsfehlercodes](activation-error-codes.md).

## <a name="clients-are-not-adding-to-the-kms-count"></a>Clients erhöhen die KMS-Anzahl nicht.

Um die Clientcomputer-ID (CMID) und andere Produktaktivierungsinformationen zurückzusetzen, führst du **sysprep /generalize** oder **slmgr /rearm** aus. Andernfalls sieht jeder Clientcomputer identisch aus, und der KMS-Host zählt sie nicht als separate KMS-Clients.

## <a name="kms-hosts-are-unable-to-create-srv-records"></a>KMS-Hosts können keine SRV-Einträge erstellen.

Das Domain Name System (DNS) schränkt eventuell den Schreibzugriff ein oder unterstützt kein dynamisches DNS (DDNS). Erteile in diesem Fall dem KMS-Host Schreibzugriff auf die DNS-Datenbank, oder erstelle den SRV-Ressourceneintrag (RR) manuell. Weitere Informationen zu KMS- und DNS-Problemen findest du unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).

## <a name="only-the-first-kms-host-is-able-to-create-srv-records"></a>Nur der erste KMS-Host kann SRV-Einträge erstellen.

Wenn die Organisation über mehr als einen KMS-Host verfügt, können die anderen Hosts den SRV-Ressourceneintrag möglicherweise nicht aktualisieren, es sei denn, die SRV-Standardberechtigungen werden geändert. Weitere Informationen zu KMS- und DNS-Problemen findest du unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).

## <a name="i-installed-a-kms-key-on-the-kms-client"></a>Ich habe einen KMS-Schlüssel auf dem KMS-Client installiert.

KMS-Schlüssel sollten nur auf KMS-Hosts, nicht auf KMS-Clients installiert werden. Führe **slmgr.vbs -ipk &lt;SetupKey&gt;** aus. Tabellen mit Schlüsseln, die du verwenden kannst, um den Computer als KMS-Client zu konfigurieren, findest du unter [KMS-Clientsetupschlüssel](KMSclientkeys.md). Diese Schlüssel sind öffentlich bekannt und editionsspezifisch. Denke daran, unnötige SRV-Ressourceneinträge aus dem DNS zu löschen, und starte dann die Computer neu.

## <a name="a-kms-host-failed"></a>Ausfall des KMS-Hosts

Wenn ein KMS-Host ausfällt, musst du einen KMS-Hostschlüssel auf einem neuen Host installieren und diesen Host dann aktivieren. Stelle sicher, dass der neue KMS-Host über eine SRV-Ressourceneintrag in der DNS-Datenbank verfügt. Wenn du den neuen KMS-Host mit demselben Computernamen und derselben IP-Adresse wie denen des ausgefallenen KMS-Hosts installierst, kann der neue KMS-Host den DNS-SRV-Eintrag des ausgefallenen Hosts verwenden. Wenn der neue Host einen anderen Computernamen hat, kannst du den DNS-SRV-Ressourceneintrag des ausgefallenen Hosts manuell entfernen oder (wenn Aufräumen im DNS aktiviert ist) das DNS diesen automatisch entfernen lassen. Wenn das Netzwerk DDNS verwendet, erstellt der neue KMS-Host automatisch einen neuen SRV-Ressourceneintrag auf dem DNS-Server. Der neue KMS-Host beginnt dann mit der Erfassung von Clienterneuerungsanforderungen und beginnt damit, Clients zu aktivieren, sobald der KMS-Aktivierungsschwellenwert erreicht ist.

Wenn Ihre KMS-Clients automatische Ermittlung verwenden, wählen sie automatisch einen anderen KMS-Host aus, wenn der ursprüngliche KMS-Host nicht auf Erneuerungsanforderungen antwortet. Wenn die Clients keine automatische Ermittlung verwenden, musst du die KMS-Clientcomputer, die dem ausgefallenen KMS-Host zugewiesen waren, manuell aktualisieren, indem du **slmgr.vbs /skms** ausführst. Um dieses Szenario zu vermeiden, konfigurierst du die KMS-Clients für die Verwendung der automatischen Ermittlung. Weitere Informationen findest du im [Bereitstellungshandbuch zur Volumenaktivierung](https://go.microsoft.com/fwlink/?linkid=150083).
