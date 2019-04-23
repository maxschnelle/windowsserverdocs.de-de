# <a name="tips-and-gotchas"></a>Tipps und Gotchas

Wenn Sie mit Git vertraut sind, kann das lernen, wie Sie effektiv arbeiten frustrierend sein. Hier werden Informationen gesammelt, daher ist es einfacher, als zu finden, wenn es in die andere Informationen in diesem Handbuch enthalten ist.

## <a name="basics"></a>Grundlagen:

Befehle in diesem "Mitwirkender" Anleitung wird vorausgesetzt, Sie haben so konfiguriert, Github, um das Standard-Repository angeben, in dem Sie Dateien aus abrufen. In Github, in dem Sie Dateien von pull-Terminologie ist Ihre *upstream*. Ist, in dem Sie Dateien mithilfe von Push übertragen Ihrer *Ursprung*. 

Aufgrund der auf wie unser Repository und den Workflow so ausgelegt sind, Ihre upstream sollte so festgelegt werden das Repository, handelt es sich unter der Microsoft-Organisation - https://github.com/Microsoft/WindowsServerDocs-pr und Ihres Ursprungs sollte Ihre Verzweigung dieses Repositorys, die sich unter Ihrem eigenen Github-Konto befindet. beispielsweise https://github.com/MY-GITHUB-ALIAS/WindowsServerDocs-pr 

>Um Ihre Einstellungen zu überprüfen, geben Sie ```git config -l```. Sehen Sie sich die URLs, um sicherzustellen, dass sie auf Speicherort zu verweisen, die Sie erstellen wollten.

Einige grundlegende Branch-Tipps:

-  Arbeiten Sie in Branches, die nicht in Ihrer lokalen Kopie des Masters. Dies erleichtert die Wiederherstellung von Problemen in Ihrer Branches, und wechseln zurück zu einem Zeitpunkt geeignete, bekannte.

-  Als Grundlage für Ihre lokalen Branches einen Branch im freigegebenen, nicht auf Ihrem remotefork. Dann müssen Sie Ihre lokalen Branches in Ihrem remotefork übertragen. Aus Ihrem remotefork müssen Sie anfordern, um die Updates in Ihrer Verzweigung zusammengeführt, in das freigegebene Repository zu erhalten. Die Befehle in diesem Artikel gezeigt, wie dies zu tun.

-  Wenn Sie eine lokale Verzweigung erstellen, weist Ihr Befehl Git welche Verzweigung, die Sie auf Ihren neuen Branch basieren soll. Dies ist bei, und wie Sie Master oder eine Verzweigung Meilenstein oder ein Feature angeben. Beispielsweise wird mit diesem Befehl erstellt einen neuen Branch aus einem upstreambranch und klicken Sie dann den neuen Branch checkt, sodass Sie an der App arbeiten möchten:

        git checkout upstream/upstream-branch-name -b your-local-branch-name

Markdown-Hilfe, beginnen Sie mit diesem [Artikel](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/) in Github. Tabellen, finden Sie in diesem [eine](https://help.github.com/articles/organizing-information-with-tables/).

## <a name="gotchas"></a>Gotchas

### <a name="deleting-files"></a>Löschen von Dateien
Es funktioniert nicht um eine Datei nur aus Ihrem Dateisystem zu löschen. Git-Befehle verwenden, lassen Sie das System, das Sie wissen möchten, vorgesehen, andernfalls werden die gelöschten Dateien wahrscheinlich Zombie-Dateien, die wieder angezeigt werden. Und nie an ein guter Zeitpunkt. Schließlich ist es möglich, dies ist ein Quellcodeverwaltungssystem und, wenn Sie es nicht, dass Sie diese Dateien entfernen möchten erkennen, es wird Hilfreicherweise den Befehl fügen sie wieder für Sie. Vielen Dank, Git! Anweisungen hierzu finden Sie unter [umbenennen oder außer Kraft setzen ein Artikels](rename-r-retire.md).

### <a name="merge-conflicts"></a>Konflikte zusammenführen

Wenn Sie ein Zusammenführungskonflikt erhalten, während Sie lokal arbeiten, müssen Sie entweder zu beheben, oder daraus zurück. Die Mehrzahl der Fälle empfiehlt es sich, einfach beheben, es sei denn, sie nicht die Dateien sind. Behalten Sie bedenken, wenn Sie nichts tun Sie möglicherweise blockiert Ihre Änderungen zu Ihrem Ursprung verwenden, übergeben, damit Sie etwas tun müssen.

**Gewusst wie: beheben** – Leitfaden zur Azure hat, Weitere Informationen hierzu und Anweisungen für den Konflikt aufzulösen. **Ein PR mit Mergekonflikte sollte nie akzeptiert,**. Achten Sie darauf, dass Sie den Namen der Repositorys und Verzweigungen in allen Beispielen ersetzen, wenn Sie überprüfen die [Anweisungen](https://microsoft.sharepoint.com/teams/azurecontentguidance/wiki/Pages/Resolve%20a%20local%20merge%20conflict%20yourself.aspx). 

**So sichern Sie** – Wenn die Konflikte in Dateien sind Sie nicht besitzen, oder es gibt einen Grund, Sie nicht, sie zu dem Zeitpunkt, hier die beschrieben, wie beheben können Sie sichern. Dadurch werden Ihre lokalen Satz von Dateien an die vor der Mergekonflikts aufgetreten sind zurückgesetzt. Führen Sie folgenden Befehl aus:

```git merge --abort```

Wenn Sie noch nicht bereitgestellt und committet die lokale Bearbeitung, können Sie dies jetzt tun. Aber wenn Sie diese Änderungen mit Push übertragen, und öffnen Sie einen Pull Request, der Konflikt wird wahrscheinlich wieder eingeblendet, wenn es in den Dateien mit Änderungen war. Sie müssen zu beheben, oder erhalten Sie Hilfe von anderen Personen zu beheben, bevor die Anforderung akzeptiert werden kann. Aus diesem Grund empfiehlt es sich um die Methode nur verwenden, um Ihre Sperrung aufzuheben, wenn Sie dringend Arbeit, z. B. ein kritisches Update verfügen.

