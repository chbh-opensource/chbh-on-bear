# Running VSCode on a compute node

It is possible to connect to a running compute node and run Visual Studio Code to test and modify your scripts. This may be useful for interactive work, testing new scripts, debugging, etc. that may require more computing resources.

It also allows you to run your scripts without needing to use `sbatch` (although that is still the preferred way for long running and array jobs).

Per the BEAR docs: 
> This allows you to run Visual Studio Code (VS Code) locally to debug the code you are running on BlueBEAR. This method is better than using the Remote SSH extension, which runs the VS Code server on a login node where the server process may be de-prioritised and killed by the system if it consumes too much resource. The Remote Tunnels extension runs the VS Code server on a compute node, which is more suitable for this purpose.

In other words, you can run VSCode interactively on a running compute node to take advantage of the greater computational power, and without needing to use `sbatch`. For example, fMRIPrep or MNE often rely on high memory usage to work correctly. 

For information on how to set this up, see the *Remote Tunnels* section of the BEAR docs: <https://docs.bear.bham.ac.uk/bluebear/vs-code-tunnel/>
