
<h>Flint Example module</h>

Description: The test module in Flint is the simple module used for understanding the flint module. It consists of 3 pools in which carbon flow happens from one pool to another. The simulation takes place in 60 steps and each step, we can see that the sum of carbon in all the pools adds up to the same number which must be the case according to the conservation of mass of carbon

This simulation uses 2 config files: nothing but the JSON files that act as input files to the model. 

It has several external dependencies 
4 header files
_module.base_exports
errorscreenwriter
libraryfactory
timeseriestransform
3 CPP files
errorscreenwriter
libraryfactory
Timeseriestransform


Point_example.json
This is one of the config files which actually act as input file for our simulation model.
It has various quantities mentioned there which acts as the parameters for the model.

Some of the parameters are mentioned here. It has 
  "type": "point"
 This tells that the simulation is point simulation
   "start_date": "1920/01/01",
This is the start date for the simulation
   "end_date": "1924/12/31",
This is the end date for the simulation
   "sequencer_library": "internal.flint",
This variable describes the sequencer library mentioning that it was internal flint
    "sequencer": "CalendarSequencer",
The calender sequencer plays an important role in steps. The steps we follow during the simulation are based on start and end date parameters of the model and they will follow in a calender sequence 
    "simulateLandUnit": "simulateLandUnit",
    "landUnitBuildSuccess": "landUnitBuildSuccess",
    "operationManager": {
     "name": "Simple",
     "use_kahan": false,
     "allow_zero_result_transfers": false
     "landUnitBuildSuccess": true
The above parameters are describing various setting of the model 
    { "Pool 1": 100.0 },
    { "Pool 2": 100.0 },
    { "Pool 3": 100.0 }
These are the initial amount of carbon in each pool
  "landUnitArea": 1.0
The unit area that needs to be considered using the simulation


The above are some of the parameters that are mentioned in the point_example.json 
Control Flow 
Starts with config files (2 files - point_example.json, libs.base.win.json)
Gets the configuration for the model from logging.debug_on.conf file
Configures the input from JSON files mentioned above (JSON2ConfigurationProvide)
LibraryManager  - loading the internal library parts
Register various things in the module 
getFlintModuleRegistrations
getFlintTransformRegistrations
getFlintFlintDataRegistrations
getFlintFlintDataFactoryRegistrations
getProviderRegistrations
All the above things are in the libraryfactory. cpp file
LibraryManager - to register the register providers
(Till now the file in which the program being run in libraryfactory.cpp file)
Now the steps the follow in the calendar sequence occur which results in the simulation from start to end
The results of the simulation are given to the output streamer which would be displayed for us as output and also we also record the output in csv files in run_env folder        


Results:
Simulation results

Description About the simulation result:
The above picture shows the simulation result obtained in the output window of vs code after executing the simulation. The same set of results would be stored in the CSV file in run_env


You can see the last 3 numbers are the carbon quantity in the pools (that is pool 1, pool 2, pool 3). This data would be saved in the CSV file in the run_env which can act as an input file for the python

By using the csv library, we can import the modules and by using the matplotlib in python we can draw the plot 



The above is the plot obtained from the test module simulation
Red line - Carbin in pool 1
Green line - Carbin in  pool 2
Blue line - Carbin in  pool 3
Yellow line - The sum of carbon in all pool (Pool 1+Pool 2+Pool 3)



