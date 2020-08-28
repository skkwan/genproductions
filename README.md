# genproductions
Generator fragments for MC production

The package includes the datacards used for various generators inclusing POWHEG, MG5_aMC@NLO, Sherpa, Phantom, Pythia...

Further details are reported in the twiki: https://twiki.cern.ch/twiki/bin/view/CMS/GeneratorMain#How_to_produce_gridpacks

Instructions on how to use the fragments are here https://twiki.cern.ch/twiki/bin/view/CMS/GitRepositoryForGenProduction

## My instructions for h->aa
### Set-up on lxplus 6 (do only once)
From lxplus6 (ssh -Y username@lxplus6.cern.ch) , follow the instructions in https://twiki.cern.ch/twiki/bin/viewauth/CMS/QuickGuideMadGraph5aMCatNLO#Quick_tutorial_on_how_to_produce to get a genproductions area:
```
mkdir mygridpack_area
cd mygridpack_area
git clone git@github.com:cms-sw/genproductions.git genproductions
cd genproductions/bin/MadGraph5_aMCatNLO/
```

### Go to the bbtautau area to generate input files for all mass scenarios:

```
cd cards/production/2017/13TeV/bbtautau_final_state/
```

``
bash createCards_ggh01_M125_Toa01a01_Tobbtautau_2017.sh
bash createCards_vbfh01_M125_Toa01a01_Tobbtautau_2017.sh
bash createCards_Wh01_M125_Toa01a01_Tobbtautau_2017.sh
bash createCards_Zh01_M125_Toa01a01_Tobbtautau_2017.sh
```

### Generate a gridpack
(this can take long and fail for no reason, you can retry the same command if it has failed)

For one mass point:
```
cd ../../../../..
./gridpack_generation.sh ggh01_M125_Toa01a01_M40_Tobbtautau cards/production/2017/13TeV/bbtautau_final_state/ggh01_M125_Toa01a01_Tobbtautau/ggh01_M125_Toa01a01_M40_Tobbtautau
```

One script that takes care of all mass points for one process (I did WH and ZH):
```
source generate_gridpacks_2016_WH.sh
source generate_gridpacks_2016_ZH.sh
```

## My instructions for h->a1a2

### Go to the bbtautau area to generate input files for all mass scenarios:
```
cd cards/production/2017/13TeV/bbtautau_final_state/
```

For **non-cascade** scenarios (M2 < 2 M1), type the mass points into `noCascadeMassPoints.txt`, 
and create the datacards like so (only WH and ZH shown):
```
source createCards_Wh03_M125_Toh01h02.sh
source createCards_Zh03_M125_Toh01h02.sh
```

For **cascade** scenarios (M2 > 2 M1), type the mass points into `cascadeMassPoints.txt`,
and create the datacards like so (only WH and ZH shown):
```
createCards_Wh03_M125_Toh01h02_h02_Toh01h01.sh
createCards_Zh03_M125_Toh01h02_h02_Toh01h01.sh
```

The output datacards are in `Wh03_M125_Toh01h02/cascades` and `Wh03_M125_Toh01h02/no-cascades` etc.


### Generate a gridpack (work in progress)