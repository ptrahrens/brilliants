# Introduction #

This language was created as a way to represent a DTSP. It can also be used to run multiple tests of the code. It is an alternative to the command-line prompts when specifying parameters.
A sample is given at the bottom of the page.

# Details #

**Ant Farm Test Harness Scripting Language**

Note int, float, string and eoln (end of line) are primitives.

testscript:
> system testparameters metrics writefile problem

system:
> SYSTEMS eoln

testparameters:
> TEST\_PARAMETERS eoln
> TEST\_PARAMETERS eoln testparams

testparams:
> testparam
> testparam testparams

testparam: one of
> paramname display refresh stop

paramname:
> param range

param:  one of
> rho alpha beta Q zeta

range:
> (init;increment;end)

init: one of
> int float

increment: one of
> int float

end: one of
> int float

display:
> DISPLAY displaypheromone displayparams
> DISPLAY displaypheromone

displaypheromone:
> bool

bool: one of
> ON OFF

displayparams:
> displayparam
> displayparam displayparams

displayparam:
> PHEROMONES = bool
> TOUR = bool
> STAGNATION = bool

refresh:
> REFRESH\_RATE int

stop:
> STOP\_CRITERIA TIME\_LIMIT int

metrics:
> metric
> metric metrics

metric: one of
> global\_best\_ant\_tour\_length
> iter\_best\_ant\_tour\_length
> lambda\_branching\_factor
> pheromone\_limit\_stagnation
> pheromone\_entropy\_stagnation



writefile:
> WRITE\_FILE filename

filename:
> string

problem:
> PROBLEM eoln probfile change
> PROBLEM eoln probfile

probfile:
> PROBLEM\_FILE tspfile eoln

tspfile:
  * tsp

change:
> CHANGE time changespecs eoln

changespecs:
> changespec
> changespec changespecs
changespec:
> add
> remove
> ispec
> remove\_add
> add\_remove

add:
> +[x\_coordinate,y\_coordinate,cityname]

x\_coordinate:
> int

y\_coordinate:
> int

remove:
> -[cityname](cityname.md)

ispec:
> i[TIME\_LIMIT,int]
> i[REPEATED\_RESULT\_LIMIT,int]

add\_remove:
> +-[tspfile,numcities,remtime,remcmds]

remove\_add:
> -+[numcities,remtime,remcmds]

numcities: one of
> int range

remtime: one of
> int range

remcmds:
> remadd
> remremove
> remispec


remadd:
> +{x\_coordinate!y\_coordinate!cityname}

remremove:
> -{cityname}

remispec:
> i{TIME\_LIMIT!int}
> i{REPEATED\_RESULT\_LIMIT!int}

**Sample Test File**

SYSTEMS
Elitist\_Ant\_System<br>
TEST_PARAMETERS<br>
PARAMETER rho (0.1;0;0.1)<br>
TRIALS 10<br>
DISPLAY ON PHEROMONES=ON TOUR=ON<br>
REFRESH_RATE 1<br>
METRICS<br>
glob_best_ant_tour_length<br>
iter_best_ant_tour_length<br>
lambda_branching_factor<br>
WRITE_FILE /home/peter/Desktop/comparative_qa194_vartime<i>-+</i>results50 WRITE CONTINUOUS<br>
PROBLEM<br>
PROBLEM_FILE /home/peter/Desktop/qa194.tsp<br>
CHANGE 0 -+[50,(0;10;60),i{TIME_LIMIT!100}]<br>