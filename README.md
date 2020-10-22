# README

Web services used by our Radio Recommendation system.

## How to start the services

Python 3 is a requirement.

The services are developed using a Jupyter notebook, to make development and iteration easier and faster. These advantages take their toll later, when the services have to be deployed in a server.

1. Execute `python3 -m pip install jupyter_kernel_gateway` to install the [Jupyter Kernel Gateway][jkg], a web server that provides headless access to Jupyter kernels.
2. Execute `jupyter kernelgateway --generate-config` to generate the configuration file for Jupyter Kernel Gateway in a folder inside the user you are issuing these commands with.
3. Edit the configuration file **~/.jupyter/jupyter_kernel_gateway_config.py**. Add the following lines:

    ```bash
    c.KernelGatewayApp.ip = '*'
    c.KernelGatewayApp.port = 9090
    ```

    The first one tells Jupyter Kernel Gateway to listen on every available IP. It should allow you to access the service from outside the server. It may be a good idea to limit access to those consuming the service.

    The second one sets the port the service will listen from.

    A personal advice here: I like keeping these lines close to the original ones, leaving them commented out. For example, the one related with the IP looks something like this in my case:

    ```bash
    ...
    ## IP address on which to listen (KG_IP env var)
    #c.KernelGatewayApp.ip = '127.0.0.1'
    c.KernelGatewayApp.ip = '*'
    ...
    ```

4. Execute [`screen`][screen]. We are going to let Jupyter running as long as needed.
5. Start the services with the command `jupyter kernelgateway --KernelGatewayApp.api='kernel_gateway.notebook_http' --KernelGatewayApp.seed_uri='/home/radiorecs/RadioRecsServices/RS.ipynb'`. In this example, the name of the Linux user is **radiorecs**, as can be seen in the last parameter passed to Jupyter.
6. Deatach from the screen session with the combination `Ctrl+a d`. That is, press `Ctrl` and `a` keys together, release them and then press `d`. That's all. You can attach to the screen later with the command `screen -r`.

[jkg]: https://jupyter-kernel-gateway.readthedocs.io/en/latest/ "Jupyter Kernel Gateway is a web server that provides headless access to Jupyter kernels"
[screen]: https://linuxize.com/post/how-to-use-linux-screen/ "How To Use Linux Screen"
