-------------------
DeBias source code
February 1st, 2017
  Assaf Zaritsky
assafzar@gmail.com

Decouples global bias from direct interactions in co-orientation and co-localization data. 
Webserver: https://debias.biohpc.swmed.edu/
This repository includes DeBias' Matlab source code and test data
-------------------

Apply DeBias:
------------
% Calculate GI and LI with DeBias for a set of observations x, y, output plots to outDname
% The only required parameters are x,y,isCoOrientation, see documentation in the code regarding default values
[GI,LI] = executeDebias(x,y,isCoOrientation,outDname,name,k,nSimulations)

% Execute DeBias on all files in a directory. 
% Supports input file formats .xls, .txt (two columns with the matched x,y observations) and .mat (variables x,y with the matched observations).   
executeDebiasDirectory(dname,isCoOrientation,k)

Simulations:
-----------
% Generate X,Y values through simulations and use executeDebias 

% Co-orientation simulation (see Figure 1B):
[X,Y] = generateCoOrientSimulationData(muX,sX,muY,sY,alpha,N);

% Colocalization simulation (see Appendix 3 - figure 1A):
[X,Y] = generateColocSimulationData(sX,sZ,N,fracColoc)

Example data:
------------
% Avaialble at the testData folder. 3 examples for co-orientation and 1 for co-localization.

% The most recommended way to start working with the source code is to generate simulated data and try DeBias on it. For example:
[X,Y] = generateCoOrientSimulationData(0,30,0,30,0.3,1000);
[GI,LI] = executeDebias(X,Y,true);

DeBias Analyst:
--------------
% Compares multiple GI,LI values derived from two different experimental conditions. 
% Outputs (GI,LI) plots (such as in Fig. 3D in the manuscript) and statistical significance of the GI and LI values across these conditions.
% See documentation in the code for details
[GIpval,LIpval] = DeBiasAnalyst(GIs1,LIs1,GIs2,LIs2,str1,str2,outdir);


Automatic estimation of K:
-------------------------
% Estimate K (number of histogram bins for EMD calculations) using the Freedman Diaconis rule.
% DeBias' ability to discriminate between different experiemtnal conditions are not sensitive to the choice of K 
% (In the manuscript: Figure 3 - figure supplement 1D-E, Figure 6 - figure supplement 1I-J, Appendix 2 - figure 2, Appendix 3 - figure 1F).
% This function is provided for the curious user ;-)
% data - is the alignment data
K = DeBiasGetK(data,isCoOrientation)

------------------
A webserver implementing this code is available at https://debias.biohpc.swmed.edu/, a comprehensive user manual is available at the web-site. 

Please cite the following manuscript when using the DeBias software:
"Decoupling global biases and local interactions between cell biological variables"
A Zaritsky, U Obolski, Z Gan, CR Reis, Y Du, SL Schmid, G Danuser
bioRxiv, http://dx.doi.org/10.1101/038059

Source code of the database and for setting the webserver are also available upon request.

Please contact Assaf Zaritsky, assafzar@gmail.com, for any questions / suggestions.