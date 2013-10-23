Marconi
=======

Message queuing service for OpenStack

Running a local Marconi server with MongoDB
-------------------------------------------

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

6. Change directories to your local copy of the repo::

    $ cd marconi

7. If you are not using a tool like `pyenv`_ with `virtualenv`_ for this then
   you may need to use sudo on the following command(s)::

    $ pip install -r requirements.txt
    $ python setup.py develop

8. (Optional) Run the following so you can see the results of any changes you
   make to the code, without having to reinstall the package each time
   (pyenv may require a rehash)::

    $ pip install -e .

8. Setup the logging folder and permissions (adjust the permissions to the
   account that will run Marconi)::

    $ sudo mkdir /var/log/marconi/
    $ sudo chown [USER THAT WILL RUN MARCONI] /var/log/marconi/

9. Start the marconi server::

    $ marconi-server

10. Test out that Marconi is working with a health check which should return an
    HTTP 204::
    
    $ curl -i -X GET http://127.0.0.1:8888/v1/health

**Note:** Keep in mind these instructions are not for a
production deployment.

.. _`Install mongodb` : http://docs.mongodb.org/manual/installation/
.. _`pyenv` : https://github.com/yyuu/pyenv/
.. _`virtualenv` : https://pypi.python.org/pypi/virtualenv/
