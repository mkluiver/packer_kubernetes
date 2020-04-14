

# Installeer Packer: #
* Installeer eerst Packer, deze is voor verschillende OS'en beschikbaar en kan gedownloade worden op https://packer.io/downloads.html (Deze installatie is getest met de Linux en Mac versie)
    * Voor Linux, download de binary file, pak hem uit, maar hem executable en verplaats hem naar /usr/local/bin/packer
    * Voor Windows, download de file en plaatse deze onder een zelf aan te maken folder Packer in C:\Program Files\Packer. Maak vervolgens een path verwijzing zodat de executable uitgevoerd kan worden.

# Voorbereiding: #
Pas de benodigde variabelen aan in de ubuntu1804.json file 
    
    Ga naar de sectie genaamd variables, en pas de nodige variabelen aan, zoals de vcenter connectie gegevens en datastore

# Installatie Kube master #

Ga met een Terminal of DOS/Powershell prompt naar de ubuntu folder (waar ook de ubuntu1804.json file staat)

    
    Voer het volgende commando uit "packer build -var vm-name=kube-master ubuntu1804.json"  (waarbij de vm-name een variabele waarde is, dit wordt en de VM naam en de hostnaam)
    De eerste keer zal deze het Ubuntu iso bestand, de VM wordt aangemaakt en gestart, en een preseed.cfg file installatie
    Daarna zal Ansible geinstalleerd worden, voert het playbook uit en daarna zal hij opschonen en de VM uitzetten.

    Zet de Kube-Master VM aan, en volg daarna Installatie Kube Nodes

    ** LET OP, op Windows krijg je een allow Windows Security alert, allow deze zodat de http server bereikbaar is.

# Installatie Kube Nodes #

Ga met een Terminal of DOS/Powershell prompt naar de ubuntu folder (waar ook de ubuntu1804.json file staat)

    
    ** Voer het volgende commando uit "packer build -var vm-name=kube-node1 ubuntu1804.json"  (waarbij de vm-name een variabele waarde is, dit wordt en de VM naam en de hostnaam)
    De eerste keer zal deze het Ubuntu iso bestand, de VM wordt aangemaakt en gestart, en een preseed.cfg file installatie
    Daarna zal Ansible geinstalleerd worden, voert het playbook uit en daarna zal hij opschonen en de VM uitzetten.

    ** LET OP: op Windows krijg je een allow Windows Security alert, allow deze zodat de http server bereikbaar is

    ** Herhaal bovenstaande stap voor elke node die je wilt toevoegen, zorg wel dat de opvolgende vm-name de term node bevat. (dus kube-node2 etc)

# Na de installatie #

* Verwijder het print-joincommand.sh script uit de packer folder, deze staat onder de folder join-command.
* Tijdens de installatie wordt een gebruiker met gebruikersnaam Ubuntu aangemaakt. Ook wordt een public key geinstalleerd. De private key (id_rsa) staat in root folder. Kopieer deze lokaal naar de ~/.ssh folder. Er kan nu een wacthwoordloze ssh connectie opgezet worden. 
* Maak een ssh connectie naar de kube-master node. Je kan nu onder de gebruiker ubuntu met kubectl aan de slag.

# Mogelijke foutmeldingen: #

Booting the VM failed -> Controleer de connectie naar de vCenter


# Geavanceerde instellingen: #

Het standaard wachtwoord voor de ubuntu gebruiker is Password!01, het kan de installatie gewijzigd worden.
