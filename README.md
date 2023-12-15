# GreenhouseDT

_note: for the on-going review, the referenced repositories are all anonymized_ 

The GreenhouseDT exemplar is a low-cost system to compare and share research on self-adaptive digital twins, with a focus on adaptation of the configuration.
The exemplar is distributed in two ways. 

 * A virtual machine available (here) that runs all components (username: lab, password: lab), and
 * A [physical setup](https://github.com/sievericcardo/greenhouse_dt_project) and two open source components for the [frontend](https://github.com/sievericcardo/greenhousedt_frontend) the [simulation driver](https://github.com/sievericcardo/smol_scheduler). These three repositories contain all the information to manually setup the system. The virtual machine is build by cloning these repositories.

The following are the guides to setup the VM and reproduce the claims of the accompanying paper.

# Reproduce
 * To visualize the prerecorded scenario (section 6), start the VM _as described below_ with the demo configuration and follow the instructions therein to start the frontend and trigger self-adaptation by issueing a query to add a plant.
 * To investigate the extensions of section 6.1 and 6.2, we refer to the [code documentation](https://github.com/sievericcardo/smol_scheduler/blob/master/demo/README.md) in the repository of the simulation driver.


# Setting up the Virtual Machine
The following are the instructions to setup the VM.
The system is already setup, but can be either run in a demonstration configuration, or a live configuration. Run the script on the desktop first.

## Setting up the environment for the demonstration configuration

The environment on the Virtual Machine is set up to use the demo environment with prerecorded data. 

- The Demo bucket of the InfluxDB instance will be used.
- The prerecorded data from the Demo bucket will display moisture information in the frontend.

## Setting up the environment for the live configuration

To use the environment with a proper greenhouse, two things has to be done

- Set up the proper token for the simulation driver; this can be done from the folder `SimulationDriver` on the Desktop and changing the settings of the `config_local.yml` file
- change the execution mode for the frontend. This can be done from the terminal with `sudo bash change_parameters.sh` and choosing the Operating Mode to either `demo` or `greenhouse`

![Change the token in case of mode](images/token-setting.png)

## Adding the RDF for the execution
In either configuration, the asset model must be uploaded.

To do so, navigate to the page `http://localhost:3030`, click on **Add Data** and **Select Files**, navigate to `home -> Desktop -> Simulation Driver` and choose the `greenhouse.ttl` if you want to use our asset model, or upload your own if you have a different one. Once you have selected the file click on **Upload Now** to upload the data; if there were no error in the file the bar will be completely green and it will show the number of triples added.

![Upload the TTL](images/ttl-upload.png)

## Executing the project

For the execution the file `execute_simulation.sh` has been added on the Desktop. You just need to execute it with the regular user with

> `./execute_simulation.sh start`

and the status the system will be updated over time on the frontend at `http://greenhousedt.local`. The complete output of the execution can be inspected in the file under `/model/model.txt`

## Extend the Greenhouse

In case of addition of elements the following file has to be modified

- `config_shelf_*`: for each shelf we use a different file and modifications and/or addition has to be added before restarting the system to get the new elements
- the asset model has to be updated with the appropriate query: this can be done on the update seciton on `http://localhost:3030`

For detailed instructions on extending the greenhouse, as well as a detailed description of the two extensions mentioned in the accompanying paper, we again refer to the [code documentation](https://github.com/sievericcardo/smol_scheduler/blob/master/demo/README.md) in the repository of the greenhouse.
