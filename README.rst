Marconi
=======

Message queuing service for OpenStack

Running a local Marconi server with MongoDB
-------------------------------------------

**Note:** These instructions are for running a local instance of Marconi for
testing or development work, it is not meant as a production deployment
installation guide.

1. `Install MongoDB`_
2. Start a MongoDB instance::

    $ mongod

3. From your home folder create the **~/.marconi** folder and clone the repo::

    $ cd
    $ mkdir .marconi
    $ git clone https://github.com/openstack/marconi.git

4. Copy the Marconi config files to the directory **~/.marconi**::

    $ cp marconi/etc/marconi-proxy.conf-sample ~/.marconi/marconi-proxy.conf
    $ cp marconi/etc/marconi-queues.conf-sample ~/.marconi/marconi-queues.conf
    $ cp marconi/etc/logging.conf-sample ~/.marconi/logging.conf

5. Find the ``[drivers:storage:mongodb]`` section in
   **~/.marconi/marconi-queues.conf** and modify the URI to point 
   to your local mongod instance::

    uri = mongodb://localhost
    
6. For logging, find the ``[DEFAULT]`` section in
   **~/.marconi/marconi-queues.conf** and modify as you wish::

    log_file = server.log    

7. Change directories to your local copy of the repo::

    $ cd marconi

8. Run the following so you can see the results of any changes you
   make to the code, without having to reinstall the package each time::

    $ pip install -e .

9. Start the marconi server::

    $ marconi-server

10. Test out that Marconi is working with a health check which should return an
    HTTP 204::

    $ curl -i -X GET http://127.0.0.1:8888/v1/health

.. _`Install mongodb` : http://docs.mongodb.org/manual/installation/
.. _`pyenv` : https://github.com/yyuu/pyenv/
.. _`virtualenv` : https://pypi.python.org/pypi/virtualenv/
