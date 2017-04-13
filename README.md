# Exact-Diagonalization-Anderson-impurity-model

Solves the Anderson Impurity model with one impurity site and Nb discrete bath sites in a star geometry for a total number of site Ns=1+Nb.

# <a href="https://github.com/L-F-A/img/blob/master/StarGeometry.jpg" /></a>

![My image](https://github.com/L-F-A/img/blob/master/StarGeometry.jpg)

The Hamiltonian is:

<a href="https://www.codecogs.com/eqnedit.php?latex=H=\sum_{\sigma}\varepsilon_dd_{\sigma}^{\dagger}d_{\sigma}&plus;Ud_{\uparrow}^{\dagger}d_{\uparrow}d_{\downarrow}^{\dagger}d_{\downarrow}&plus;\sum_{i,\sigma}\varepsilon_ic_{i\sigma}^{\dagger}c_{i\sigma}&space;&plus;\sum_{i,\sigma}V_i\left(&space;d_{\sigma}^{\dagger}c_{i\sigma}&plus;c_{i\sigma}^{\dagger}d_{\sigma}\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?H=\sum_{\sigma}\varepsilon_dd_{\sigma}^{\dagger}d_{\sigma}&plus;Ud_{\uparrow}^{\dagger}d_{\uparrow}d_{\downarrow}^{\dagger}d_{\downarrow}&plus;\sum_{i,\sigma}\varepsilon_ic_{i\sigma}^{\dagger}c_{i\sigma}&space;&plus;\sum_{i,\sigma}V_i\left(&space;d_{\sigma}^{\dagger}c_{i\sigma}&plus;c_{i\sigma}^{\dagger}d_{\sigma}\right&space;)" title="H=\sum_{\sigma}\varepsilon_dd_{\sigma}^{\dagger}d_{\sigma}+Ud_{\uparrow}^{\dagger}d_{\uparrow}d_{\downarrow}^{\dagger}d_{\downarrow}+\sum_{i,\sigma}\varepsilon_ic_{i\sigma}^{\dagger}c_{i\sigma} +\sum_{i,\sigma}V_i\left( d_{\sigma}^{\dagger}c_{i\sigma}+c_{i\sigma}^{\dagger}d_{\sigma}\right )" /></a>

where 

<a href="https://www.codecogs.com/eqnedit.php?latex=i=2\ldots&space;N_s&space;\quad&space;\text{and}&space;\quad&space;\sigma&space;=&space;\uparrow,\downarrow&space;\quad\text{the&space;possible&space;spin&space;directions.}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?i=2\ldots&space;N_s&space;\quad&space;\text{and}&space;\quad&space;\sigma&space;=&space;\uparrow,\downarrow&space;\quad\text{the&space;possible&space;spin&space;directions.}" title="i=2\ldots N_s \quad \text{and} \quad \sigma = \uparrow,\downarrow \quad\text{the possible spin directions.}" /></a>



  - More detailed explanations to come on the model, how to use the codes and cleaning the format of the codes that I never       bother to do. 

  - While Ns=11 and Ns=12 are possible in principle (precompute the dictionary and save it), this pushes the capability very much. Ns=10 works pretty well on a desktop. For larger Ns such as 11, 12, 13, 14 (even the best implementation cannot go much larger) it does not make sense to use an implementation in Matlab or Python (this implementation could be slightly more efficient in the dictionnary for example, but I never bother pushing the efficiency to the extreme as alternative are available). Using one of the available c, c++ or Fortran implementations is suggested for Ns > 10. 
  
  - However, even without explanation on the codes, if one has a value of Ns, values for all parameters of the Hamiltonian i.e. ed,U,e_2,V_2,...,e_Ns,V_Ns, a fictitious temperature T and a number of Matsubara frequencies Nmat, Every possible quantities for the model can be obtained by running:

        wn=pi*T*( 2*(0:Nmat-1)+1 );

        [C_ind,table,indice_sector,H_non_zero_ele] = ED_Ns_generate_final(Ns);

        spar=0

        ee=[e_2,e_3,...,e_Ns];

        VV=[V_2,V_3,...,V_Ns];

        [Gcl,E,EGS,Psi,Psi_GS,NSz_GS,Problem_mat,nd,ndup,nddown,nc,ncup,ncdown,D,an_m,bn2_m,dplusd,an_p,bn2_p,ddplus] =      ED_Green_final(wn,ed,U,ee,VV,Ns,C_ind,table,indice_sector,H_non_zero_ele,spar)

        Gcl is the Green's function of the impurity
        E contains the smallest energies of each sector
        EGS is the ground state energy
        Psi contains the wave functions corresponding to E
        Psi_Gs is the ground state wave function
        NSz_GS informs about which sector has the ground state in [N,Sz] N electrons with total Sz spin
        nd is the impurity electronic density
        ndup is the impurity electronic density with spin up
        nddown is the impurity electronic density with spin down
        nc,ncup,ncdounw the same for the bath
        D is the double occupy of the impurity
        an_m,bn2_m,dplusd,an_p,bn2_p,ddplus are the continued fraction coefficients of the Green's function

These codes were used in https://arxiv.org/abs/1408.1143 and https://arxiv.org/abs/1506.08858 .
