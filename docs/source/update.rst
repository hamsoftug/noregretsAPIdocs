Update
======

.. NOTE:: We recommend you having a backup your of your SMS database with all status.

To update your CRM got to **Settings > System info** and click on **Schedule Update**.  
Enter the time when the app should update and timezone.

.. attention:: All Your requests  will be set to maintanance mode and maintanance status codes deisplayd when performing an update to the API and restored after the update process has completed.

If you're moving your messages and receivers to another provider or servers make sure to request that data with the provided endpoints.

You can manually run the update with the following command.

.. code-block:: messages

	GET /api/v1/invoices
  Accept: application/json
  Authorization: Key: $ApiKey

``GET`` - /api/v1/messages/

.. TIP:: You can see the detailed `changelogs </changelog.html>`_ for each release.

Version 2.0
"""""""""""

Copy .env.example to .env and set config settings

Check that ``/path/to/workspace/storage`` has 755 permissions and is owned by the webserver user
