# Kinetic database carbfix_kin.dat / carbfix.dat
This database is an extended version of the [carbfix.dat](https://github.com/CarbFix/carbfix.dat) thermodynamic database for [PHREEQC](https://www.usgs.gov/software/phreeqc-version-3) that includes a kinetic database for selected primary and secondary mineral dissolution.

Reference literature for derived kinetic fits can be found in [Hermanska et al. (2022)](https://doi.org/10.1016/j.chemgeo.2022.120807), along with pH and temperature conditions. Please note that extrapolation of the database to different conditions or mineral precipitation might lead to incorrect results.  

The kinetic database contains a list of mineral dissolution parameters in the form of RATES blocks for PHREEQC. When loading this database in PHREEQC, simulations can make use of them through using KINETICS blocks.

## Examples
Below are minimal examples for such a KINETICS blocks, explaining the different parameters specific to the database. Other parameters can be specified as explained in the PHREEQC documentation.

```
#Example data block for mineral end-members:

KINETICS
Albite                                     # Name of the mineral
    -m0        1e-3                        # Initial moles of mineral
    -parms     0 100 0                     # Three parameters as explained below



#Example data block for selected mineral solid solutions (selected solid solutions listed in Appendix in Hermanska et al. (2022)):

KINETICS
Augite_ss                                  # Name of the mineral
    -formula  Mg0.45Fe0.275Ca0.275SiO3  1  # Mineral formula 
    -m0       100                          # Initial moles of mineral
    -parms    0 0.0088183 0                # Three parameters as explained below



#Example data block for basaltic glass:

KINETICS
Glass_Basalt                                                            # Name of phase
    -formula    SiTi0.02Al0.36Fe0.19Mg0.28Ca0.26Na0.08K0.008O3.364 1    # Glass formula
    -m0         1e-3                                                    # Initial moles of mineral
    -parms      0 100 0                                                 # Three parameters as explained below
```
### Parameters

Three parameters are necessary when using rates:

 - The first parameter specifies if the specific surface area is entered as m2 per g of rock (0) or m2 per kg of water (1)

 - The second parameter specifies the specific surface area of the mineral (in m2/g or m2/kgw depending on the choice of the first parameter)

 - The third parameters define how the surface area changes during dissolution and has three possible values. This option is only available when the first parameter is 0. If the first parameter is 1, the surface area is always constant.
   0: The surface area changes linearly with the moles of the mineral present
   1: The surface area changes according to the geometry of dissolving cubes or spheres
   
   
## References
For a detailed description and for citing the source when using it in your own work, please refer to the following literature for the kinetic and thermodynamic parts of the database, respectively:

*Hermanska M., Voigt M. J., Marieni C., Declercq J., and Oelkers E. H. (2022) "A comprehensive and internally consistent mineral dissolution rate database: Part I: Primary silicate minerals and glasses" Chemical Geology, doi:[10.1016/j.chemgeo.2022.120807](https://doi.org/10.1016/j.chemgeo.2022.120807)*

*Voigt, M., Marieni, C., Clark, D. E., Gíslason, S. R., and Oelkers, E. H. (2018) "Evaluation and refinement of thermodynamic databases for mineral carbonation" Energy Procedia 146, 81-91, doi:[10.1016/j.egypro.2018.07.012](https://doi.org/10.1016/j.egypro.2018.07.012)*
