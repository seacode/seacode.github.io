# Gmacs Progress Report September 2014
### by Athol Whitten, with Jim Ianelli and Andre Punt

## Gmacs Project Overview

3. Gmacs will remain at Seacode, the Council will decide who 'manages' the code.

Recommomendations for management:
  * NOAA should maintain some involvement: but should be one player rather than the sole. Thus, ADFG, SARDI, etc. 
  * Crab Plan Team could designate people who are 'the gate keepers', this could be the top level above the 'developers' list. 
  * Feeds into discussion about other software, Buck's Tanner model for example could sit alongside Gmacs, and used for multi-model inference at assessment time.
  * Independent people could be sub-contracted to do large pieces of coding as requested/identified by the CPT.


## Gmacs

1. Can we now rename Gsmac to Gmacs? 
  * What is the process for doing this wrt Github?

2. Run through the TODO list on the Github Site.
  * See `WhittenDeveloper` Branch for updated README and TODO

* Makefile needs to be made platform agnostic: Jim will work on this. There is only one makefile in the gmacs/src directory now. 


### BBRKC Example

Jie has provided more information regarding his (ADFG) BBRKC model specific to the use if weight- and fecundity-at-size information. The information has been summarised in the `README.me` file in the Gmacs Shared Folder under ADFG. 

### Documentation

1. Idea: produce a general paper (technical document) that could be published (PlosONE) and serve as the first reference for Gmacs. The existing Word Document can be converted to Latex (then MD) as a starting point.
2. Github:
  * Github Wiki: Servers as a User Guide. i.e. 'How to make the model run', and can be turned into a PDF for distribution as required.
  * Github README: Serves as a general overview and starting point
3. Doxygen generated documentation. This needs work.
4. Second paper using Gmacs for reasearch: Size-classes simulation. Submit to CAPAM Growth Workshop.

### R Package

1. The R package `gmr` is now setup and working with a few minimal examples at https://github.com/seacode/gmr 
2. The R package code files have internal Roxygen comments to generate documentation.
3. R Package code follows the 'Advanced R Style Guide' by Hadley Wickham

# Cstar

* What portions of Gmacs code should be moved to Cstar?
* Rstar is R code in support of Cstar: Shiny might work well here.

Cstar needs some attention, the functions in Gmacs/src at the moment.  

# Extra Notes:

# Sim Flag will call simulation_model() function. 

This, at the moment, using a rmv_logistic() function. This is a mismatch to the 'default' distribution assumption of the estimation model, which uses an assumed multinomial() distrubution when determining the predicted catch comp observations.

--------------------------
Notes on gmacs.tpl (new)

INITIALIZATION_SECTION
  First 5 parms: are read in at this point, at the moment they are fixed values for the BBRKC model, so need to be made part of the control file.


FUNCTION calc_fishing_mortality
  For years and gears for which there is catch data, F values are estimated directly. Thus, in the data, catches or zero, can be entered, or not, both will work, but zeros will be ignored. 

  TODO, the model does not currently accommodate situations where there is data on effort but not on catch, nor where there is effort and a recorded zero catch. This is a future extension option.


 GENERAL NOTES
  Old shell, new shell, infrastructure exists, but is not working yet. This is a major priority.

  The next is adding time-varying options for M and other things not yet set-up, seems selex is the only one now with time-varying options now.

  Growth is in the code now, should go to Cstar. There is also no time-varying growth, that should be added as a second level priority.

  At is used twice, once in the update_population and equil_conditions section, as the name for the transition matix. It is A, then the transpose of A. Which one of these is reported? 

  Jim identified a penalty issue that needs to be dealt with. 

  Critical issue: need to deal with maturity- and shell-

--------------------------

DATA: CHECK JIE'S DATA: On Maturity, what information is there? Any? Answer seems to be NO.

Check ALL DATA: make sure it is being specified correctly in our new model.

Check: Fecundity vs. Maturity: The fecudnity vector that is used now, is that used for mature male biomas?

From Jie: Fecundity is not used, so ignore it anyway. Mature is binary, a step function. 1 over a certain size for males and females seperately. 

CHECK WHY ANDRE HAD/USED a FECUNDITY VECTOR? Why was it there, do we need to care.

When reviewing BBRKC models b/w ADFG and Gmacs, make this part of a document because a comparison will be required for the September meeting.

Move BBRKC folder from Projects/Cstar/Models to ./Gmacs/Models and change the name to simple_bbrkc

Work through seacode/gmacs issues and raise new given meeting outcomes

Suggest splitting current documentation into two parts, one for user guide (wiki) and another for paper (technical description)

Check for objections first: then remove depracated branches from seacode (?) can we get back to Github Workflow soon? With development going on in developer branch, and each new feature as separate branch

<!-- TODO list created by Martell and Whitten -->
### TODO List ###

#### Project
- [x] Create makefile for building and installing Gmacs (debug & release)
<<<<<<< HEAD
  - [x] Test makefile on Windows box (batch file)
- [x] Create commandline option for simulation model (-sim seedNo.)
- [ ] Perform simulation testing
- [ ] Update documentation
  - [ ] Extend existing Doxygen comments and create Doxygen output
  - [x] Continue working on Gmacs Wiki, pdf version = user-guide
- [ ] Test scripts with simulated data and examples
=======
  - [ ] Test makefile on Windows box
- [x] Create commandline option for simulation model (-sim seedNo.)
- [ ] Perform simulation testing
- [ ] Update documentation
  - [x] Extend existing Doxygen comments and create Doxygen output
  - [ ] Continue working on Gmacs Wiki, parallel with user-guide
- [x] Test scripts with simulated data and examples
>>>>>>> MartellDeveloper

#### Gmacs Executable
- [x] Get code to compile.
- [ ] Document data structures.
- [ ] Implement alternative likelihoods for composition data
- [x] Develop alternative models for time-varying parameters
- [x] Implement spline functions as alternative to 'piecewise linear' functions in current model.
- [ ] Consider cumulative normal distribution (and/or others) as alternatives to gamma function for size-at-recruitment and/or growth increment.
- [ ] Incorporate option to use tagging data to estimate growth.
- [x] Implement the capacity to change functional form for selectivity (and other factors) over time
- [ ] Implement the capacity for penalties to be placed on the extent to which parameters change over time
- [ ] Implement time-varying recruitment using deviations from a SR-relationship as alternative to using deviations from a mean
- [ ] Allow time-varying M to depdend on maturity state *and* length
- [ ] Implement **hybrid** method as an option for calculating annual fishing mortality rates
- [x] Add options for implementing cubic splines
  - [ ] splines for selectivity,
  - [ ] splines for initial size-distribution,
  - [ ] splines of time-varying parameters.

Possible things for issues list:

* Need to include molt increment data to estimate molt parameters
* Need to include Tanner by-catch data
* Switch option for calc_relative_abundance

     Try to get current checkout saved as new branch, then step up to latest changes by SM (debug), then push to developer branch, suggest scrap other branches, and move to the Gitflow program. Make announcement of this on Wiki.

OK, now in Branch: Debugger, remove DeBug and go from there.

GET JIE DATA AND CHECK SHELL TYPE

Gmacs Workflow:
PUSH NEW README FILE TO MAIN PAGE: and move towards getting Gitflow going...

2) Developers

Gmacs development is handled with the assistance of Git: a powerful and flexible version control system. Developers should follow these steps in order to successfully contribute code and improvements to Gmacs:

Download Git

Scenario: Siddeek is working on a new feature for his crab model, with aims to make it part of the core gmacs program. NPFMC policy dictates that he use the official 2014 release of Gmacs for this assessment model this year, and that any new features should be reviewed by (?)  before being adopted for assessment purposes. So in this case, he needs two copies of Gmacs on his machine, one for assessing the stock, another for development purposes.

What should his workflow look like?

what I'm not sure about is that compiler ussie mentioned above, for example, SS for windows, already behaves in the desired manner, ie: I have a bacth file sitting inside my model directory that contains the dat and ctl files, and inside the bacth file is c:/ss3/v324s/ss3.exe. Running the batch script

ISSUES WITH JIES MODEL: TOO MANY CRABS IN THE FINAL SIZE BIN for RETAINED MALES

CAN WE GET AN ORGANISATION PAGE FOR SEACODE and thus a place for GMACS INFO? Or links to downloads for .exe versions? Or link to a makefile that downloads the required files for new users and builds the cstar lib?

When can we change to developer branch, then release a version to master?
