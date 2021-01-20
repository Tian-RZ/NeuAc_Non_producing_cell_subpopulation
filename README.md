# NeuAc_Non_producing_cell_subpopulation

## Description
NeuAc biosynthesis model calculation results of fermentation in the presence and absence of non-producing subpopulations, the MATLAB code are provided as Model_Subpopulations_NeuAc_Yiled.m  

>Matlab 2019b was used to build the model. The growth curve data of the strains in the model are obtained by interpolation based on the experimental results. The proportion of non-producing cell subpopulation is calculated according to the flow cytometry results: I_Nonproducing(%) = 1.0729 * t + 17.833, R2=1 (t is the fermentation time). Since the NeuAc biosensor can only be used to analyze the distribution of the producing cell subpopulation and non-producing cell subpopulation in NeuAc synthesis performance, the NeuAc produced by producing cell subpopulation per unit time unit biomass in the model is set to 1 (arbitrary unit, a.u.).
