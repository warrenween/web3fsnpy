
.. |br| raw:: html

    <br>


Installation
============

These instructions work for Ubuntu (> v18.04) and Debian (> v10 buster). There may be some variations for other distros.

From a wheel Using pip3
^^^^^^^^^^^^^^^^^^^^^^^

Install some dependencies (you will need > python3.6) :-

.. code-block:: bash

    #> sudo apt install python3 python3-pip
    #> sudo pip3 install web3fsnpy  (or pip3 install web3fsnpy --user if you want to install a username only copy)

Quick Start
^^^^^^^^^^^
    
You can find some example python programs at :doc:`examples` 
designed to demonstrate the API's functionality. These will be added to as new functions are developed.

You will probably need to set the environmental variable FSN_PRIVATE_KEY to be able to use any write transaction methods. 
Get your private key from your Fusion wallet (click on 'View details') and then :-

.. code-block:: bash

    #> export FSN_PRIVATE_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXX
    
Alternatively you can generate your private key using your wallet JSON file and an input password. The way to do this is illustrated in :doc:`examples`

To update (frequent updates available) just type :-

.. code-block:: bash

    #> sudo pip3 install --update web3fsnpy  (or pip3 install --update web3fsnpy --user)
    
Now you need to update the PYTHONPATH environmental variable to your .bashrc file assuming that you are in the folder web3fsnpy :-

.. code-block:: bash

    #> echo "export PYTHONPATH=$PYTHONPATH:$PWD">>~/.bashrc

Now restart your shell to activate the PYTHONPATH.



Developer setup
^^^^^^^^^^^^^^^

For a developer setup, although it is not required, you will likely need to install Ethereum's web3.py according to the instructions at https://github.com/ethereum/web3.py

To install web3fsnpy :-

.. code-block:: bash

    #> git clone https://github.com/FUSIONFoundation/web3fsnpy.git

The dependencies are listed in the file requirements.txt




It is best practice to operate within a virtualenv when modifying code, so as to isolate dependency issues :-

.. code-block:: bash

    #> source env/bin/activate
    
To install the python dependencies in this virtual environment from the file requirements.txt :-

.. code-block:: bash

    #> pip3 install -r requirements.txt
    
Check that the scope includes the correct python module versions :-

.. code-block:: bash

    #> pip3 list  (or pip3 show <module name> )
    
Sometimes a pre-existing install may have a higher version number of a module, which can cause unpredictable results.


Connection to the Blockchain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are three ways to connect to the blockchain:- HTTP, WebSocket and IPC.
If your are not running a node on your machine, then WebSocket is preferred over HTTP, since it allows asynchronous bi-directional communication.

There are two 'networks' :-  'mainnet' and 'testnet'.

The 'default' 'gateway' values hardcoded into the Fsn class constructor __init__(linkToChain) method are as follows:-

WebSocket (testnet):- 'wss://testnetpublicgateway1.fusionnetwork.io:10001' |br|
WebSocket (mainnet):- 'wss://mainnetpublicgateway1.fusionnetwork.io:10001' |br|
HTTP (testnet):- 'https://testnetpublicgateway1.fusionnetwork.io:10000/' |br|
HTTP (mainnet):- 'https://mainnetpublicgateway1.fusionnetwork.io:10000/'|br|
IPC :- '/home/root/fusion-node/data/efsn.ipc'

These can all be overridden using strings


Sanity Check
^^^^^^^^^^^^

You can check that your installation has been successful as follows :-


.. code-block:: python

    >>
    #web3fusion
    from  web3fsnpy import Fsn
    
    linkToChain = {
        'network'     : 'testnet',                          # One of 'testnet', or 'mainnet'
        'provider'    : 'HTTP',                             # One of 'WebSocket', 'HTTP', or 'IPC'
        'gateway'     : 'default',                          # Either set to 'default', or uri endpoint
        #'private_key'     : os.environ["FSN_PRIVATE_KEY"],  # comment out for just read operations
    }

    #

    web3fsn = Fsn(linkToChain)
    
    print('Current block height is ',web3fsn.blockNumber)
    

   
   
    
    
