Wenn Sie ein Azure-Abonnement verwenden, für das Sie nicht als Administrator oder Besitzer fungieren (etwa ein Abonnement eines Unternehmens), überprüfen Sie vor dem Ausführen der Schritte in diesem Artikel die folgenden Punkte:

* Für die Anmeldung bei Azure benötigen Sie mindestens das Zugriffsrecht „Mitwirkender“ für die Azure-Ressourcengruppe. Diese Ressourcengruppe dient zum Erstellen eines Azure HDInsight-Clusters und anderer Azure-Ressourcen.
* Ein Benutzer, der für das Azure-Abonnement mindestens über Zugriff vom Typ „Mitwirkender“ verfügt, muss den Anbieter für die von Ihnen verwendete Ressource bereits registriert haben. Die Anbieterregistrierung findet statt, wenn ein Benutzer, der über Abonnementzugriff vom Typ „Mitwirkender“ verfügt, erstmals eine Ressource für das Abonnement erstellt. Dies kann auch ohne Erstellung einer Ressource erreicht werden. Führen Sie dazu wie [hier](https://msdn.microsoft.com/library/azure/dn790548.aspx) beschrieben eine REST-basierte Anbieterregistrierung aus.

Weitere Informationen zur Verwendung der Zugriffsverwaltung finden Sie in den folgenden Artikeln:

* [Erste Schritte mit der Zugriffsverwaltung im Azure-Portal](../articles/active-directory/role-based-access-control-what-is.md)
* [Verwenden von Rollenzuweisungen zum Verwalten Ihrer Azure-Abonnementressourcen](../articles/active-directory/role-based-access-control-configure.md)


<!--HONumber=Jan17_HO1-->


