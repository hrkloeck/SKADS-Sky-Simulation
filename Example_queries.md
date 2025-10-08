# Example Queries for SEX and SAX are listed
These were the original queries examples from the s-ccubed homepage. Everyone is wellcome to add at the bottom.

-SEX Queries

    - Get all galaxies with 1400MHz flux density brighter than 100 mJy in the central 1 square degree of the simulation   
    
      select * from Galaxies where (pow(10,itot_1400)*1000 > 100.0) and (right_ascension between -0.5 and 0.5) and (declination between -0.5 and 0.5)

    - Define an 843MHz flux density by interpolating between the 1400MHz and 610Mhz flux densities and then search for all galaxies with S_843 > 100 mJy
    
      select * from select galaxy, sftype, agntype, right_ascension, declination, distance, redshift, itot_610 + ((log10(843)-log10(610))/(log10(1400)-log10(610)))*(itot_1400-itot_610) as itot_843 from Galaxies) as temp where pow(10,temp.itot_843)*1000 > 100.0
      
    - Find the ratio of the core to the total flux density and the spectral index between 1400MHz and 610MHz for all radio-loud AGN between redshift 0.3 and 0.4
    
      select pow(10, Components.i_1400 - Galaxies.itot_1400) as c_tot_ratio, (Galaxies.itot_1400 - Galaxies.itot_610)/log10(1400/610) as sindex from Galaxies inner join Components on Galaxies.galaxy=Components.galaxy where ( Galaxies.agntype = 2 or Galaxies.agntype = 3 or Galaxies.agntype = 4 ) and ( Galaxies.redshift  between 0.3 and 0.4 ) (Components.structure=1)
      
    - Find all the galaxies in cluster number 2220 and print out some vital information including the peculiar velocity of the galaxy and the position offset of the galaxy from the center of the cluster
    
      select Galaxies.galaxy, Galaxies.cluster, Galaxies.galaxy, Galaxies.agntype, Galaxies.distance, Galaxies.redshift, (Clusters.redshift - Galaxies.redshift)*2.99792e5 as vel_offset, sqrt(pow(Clusters.right_ascension - Galaxies.right_ascension,2.0) + pow(Clusters.declination - Galaxies.declination,2.0))*3600.0 as pos_offset from Galaxies inner join Clusters on Galaxies.cluster=Clusters.cluster where Clusters.cluster=2220

    - select * from Galaxies where x < 10 and x > 9 and y < 10 and y > 9
    
    - select * from Galaxies where type =4
    
    - select * from Galaxies where i_150 > 4 and i_150 < 4.5 and i_610 > 3 and i_610 < 3.25


-SAX Queries

   - Get the position, apparent redshift, and integrated HI-flux of the 10 closest galaxies in the cone
     
     select ra, decl, zapparent, hiintflux from milli_galaxies_line order by distance limit 0,10
     
   - This query evaluates the number of sources per square degree and unit of redshift z with an HI-peak flux density above 1 micro Jansky. The evaluation is based on the central 0.6x0.6 square degrees of the mock observing cone and redshift bins of dz=0.1. The result is given for the range z=0-4
     
    select floor(zapparent*10.0+0.5)/10.0 as z, floor(count(*)*10/(0.6*0.6)) as dNdz from milli_galaxies_line where ra between -0.3 and 0.3 and decl between -0.3 and 0.3 and hiintflux*hilumpeak > 1e-6 and zapparent < 4.05 group by floor(zapparent*10.0+0.5)/10.0 order by z

    
   - This query finds the position, the extinction corrected abso
lute blue magnitude, and the first five CO-line fluxes of the galaxies in the central square degree at redshift z=1.00+-0.05, whose ex
tinction corrected absolute blue magnitude is below -22.

    select t1.ra, t1.decl, t1.zapparent, t1.cointflux_1, t1.cointflux_2, t1.cointflux_3, t1.cointflux_4, t1.cointflux_5, t2.mag_bdust from milli_galaxies_line t1, milli_galaxies_delu t2 where t1.id=t2.id and t1.ra between -0.5 and 0.5 and t1.decl between -0.5 and 0.5 and t1.zapparent between 0.95 and 1.05 and t2.mag_bdust < -22
   
   - This query finds all the galaxies in the most massive cluste r in the mock observing cone between z=1.2 and z=1.5. For each galaxy the output table gives the position, the apparent redshift, the integrated HI-flux (Jy km/s), the HI-peak flux density (Jy), the 50% HI-line width (km/s), the HI-half mass radius (arcsec), the inclination (rad), and the extinction corrected absolute blue magnitude. Only galaxies with stellar masses above 10^9 solar masses are retained.
     
     select t1.ra, t1.decl, t1.zapparent, t1.hiintflux, t1.hiintflux*t1.hilumpeak as peakfluxdensity, t1.hiwidth50, t1.himajoraxis_halfmass, t1.diskinclination, t2.mag_bdust from milli_galaxies_line t1, milli_galaxies_delu t2, select t2.fofid as maxfofid, t1.box as maxbox from milli_galaxies_line t1, milli_galaxies_delu t2,(select max(t2.mvir) as maxmvir from milli_galaxies_line t1, milli_galaxies_delu t2 where t1.id=t2.id and t1.zapparent between 1.2 and 1.5) tmp1 where t1.id=t2.id and t2.mvir=tmp1.maxmvir and t1.zapparent between 1.2 and 1.5 limit 0,1) tmp2 where t1.id=t2.id and t2.fofid=tmp2.maxfofid and t1.box=tmp2.maxbox and t2.stellarmass*1e10/0.73>1e9

# Your favouried query
