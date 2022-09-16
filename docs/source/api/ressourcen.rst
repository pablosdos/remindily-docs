.. _ressourcen:

===========
Ressourcen
===========

.. note::
    Die Ressourcen sind darauf ausgelegt, keine unnötigen Daten im Browser Cache zu erzeugen – aus Performance- und Sicherheitsgründen.

    User kann man über die Remindily-API nicht abgreifen, sie werden über Keycloak bereitgestellt. Sie tauchen lediglich der Übersicht wegen im Ressourcenpfad auf.

    Die BaseURL wird von Entwicklungs- Staging- oder Produktivumgebung vorgegeben.


Scheduler
===============================

Schedulers sind Remindilies und damit wesentlich für die Struktur der App. 

Aufrufen der Schedulers eines Users
^^^^^^^^^^^^^^^^^^^^^^^^^^

Das Abfragen aller Schedulers eines Users ist bspw. für Listenansichten im Frontend relevant. In der aktuellen Version werden alle jemals erstellten Schedulers eines Users durch diesen Endpunkt abgefragt – offene und bereits abgeschlossene.

.. code-block:: sh

    $ curl --location --request GET '<baseURL>/api/users/<userId>/schedulers' \
    --header 'Authorization: bearer <keycloakToken>'

.. code-block:: json

    {
    "schedulers": [
        {
        "id": "scheduler_1LiKea2eZvKYlo2CZ3FHqaD5",
        "userId": "scheduler_1LiKea2eZvKYlo2CZ3FHqaD5",
        "startTime": 1663258265,
        "endTime": 1663258265,
        "amountOfMails": 7,
        "createdAt": 1663258265,
        "updatedAt": 1663258265,
        "contact": {
            "id": "contact_4QFK8XrieeBDYp",
            "userId": "user_4QFK8XrieeBDYp",
            "email": null,
            "firstName": null,
            "lastName": null,
            "phone": null,
            "branche": null,
            "companyName": null,
            "createdAt": 1663258265,
            "updatedAt": 1663258265
        },
        "reminderMails": [
            {
            "id": "reminderMail_1LiKea2eZvKYlo2CZ3FHqaD5",
            "sender": null,
            "receiver": null,
            "replyTo": null,
            "mailHtml": null,
            "subject": null,
            "salutation": null,
            "content": null,
            "closing": null,
            "signature": null,
            "isSent": false,
            "createdAt": 1663258265,
            "updatedAt": 1663258265,
            "todos": [
                {
                "title": null,
                "description": null,
                "isDone": false
                }
                {...},
                {...}
            ]
            },
            {...},
            {...}
        ]
        }
    ]
    }

ReminderMail
===============================

Ein Scheduler besteht aus n ReminderMails. 

Aufrufen der ReminderMails eines Schedulers
^^^^^^^^^^^^^^^^^^^^^^^^^^

Ein Beispiel für die Verwendung dieses Endpunkts: Durch das Aufrufen aller ReminderMails der aktiven Schedulers kann der Mailserver noch nicht versandte Mails in die Warteschlange legen.

.. code-block:: sh

    $ curl --location --request GET '<baseURL>/api/user/<userId>/schedulers/<schedulerId>/remindermails' \
    --header 'Authorization: bearer <keycloakToken>'

.. code-block:: json

    {
        "schedulers": []
    }

Contacts
===============================

Ein User kann eine Vielzahl von Contacts anlegen.

Schedulers eines Users
^^^^^^^^^^^^^^^^^^^^^^^^^^

Das Abfragen aller Schedulers eines Users ist bspw. für Listenansichten im Frontend relevant. In der aktuellen Version werden alle jemals erstellten Schedulers eines Users durch diesen Endpunkt abgefragt – offene und bereits abgeschlossene.

.. code-block:: sh

    $ curl --location --request GET '<baseURL>/api/user/<userId>/contacts' \
    --header 'Authorization: bearer <keycloakToken>'

.. code-block:: json

    {
        "schedulers": []
    }
