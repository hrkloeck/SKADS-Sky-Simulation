# SKADS-Sky-Simulation

The SKA Design Study Sky Simulations (SKADS)

The SKADS Simulated Skies (S-cubed) are a set of simulations of the radio sky performed at the
University of Oxford (long time ago), suitable for planning science with the Square Kilometer 
Array radio telescope.

The radio continuum is descriped by the S-cubed-SEX (Semi-Empirical
eXtragalactic (SEX) simulation) 
[Wilman et al. 2008](https://academic.oup.com/mnras/article/388/3/1335/956611)
DM density field evolved under linear theory, populated with objects
from known radio luminosity functions, and with other important physics
(e.g. non-linear structures, source models) `
pasted on’
currently 20x20 deg2 out to z~20 ,
~2.5x108 simulated sources

Sky area: 20x20 deg2
• Redshift range: z = 0 – 20
• Flux density limits: 10nJy @ 151MHz, 610MHz, 1.4 GHz,
4.86 GHz & 18 GHz
• Source populations: radio-quiet AGN
FRI and FRII radio-loud AGN
normal star-forming galaxies
starburst galaxies



A virtual sky of extragalactic HI and CO Lines is descriped by the SAX (Semi-Analytic
eXtragalactic simulations)

[Obreschkow et al. 2009](https://iopscience.iop.org/article/10.1088/0004-637X/703/2/1890)

We present a sky simulation of the atomic HI-emission line and the first 10 CO rotational emission lines of molecular gas in galaxies beyond the Milky Way. The simulated sky field has a comoving diameter of 500 h−1 Mpc; hence, the actual field of view depends on the (user-defined) maximal redshift zmax; e.g., for zmax = 10, the field of view yields ∼4 × 4 deg2. For all galaxies, we estimate the line fluxes, line profiles, and angular sizes of the H i and CO-emission lines. The galaxy sample is complete for galaxies with cold hydrogen masses above 108 M☉. This sky simulation builds on a semi-analytic model of the cosmic evolution of galaxies in a Λ cold dark matter (ΛCDM) cosmology. The evolving CDM distribution was adopted from the Millennium Simulation, an N-body CDM simulation in a cubic box with a side length of 500 h−1 Mpc. This side length limits the coherence scale of our sky simulation: it is long enough to allow the extraction of the baryon acoustic oscillations in the galaxy power spectrum, yet the position and amplitude of the first acoustic peak will be imperfectly defined. This sky simulation is a tangible aid to the design and operation of future telescopes, such as the Square Kilometre Array, Large Millimeter Telescope, and Atacama Large Millimeter/Submillimeter Array. The results presented in this paper have been restricted to a graphical representation of the simulated sky and fundamental dN/dz analyses for peak flux density limited and total flux limited surveys of H i and CO. A key prediction is that H i will be harder to detect at redshifts z ≳ 2 than predicted by a no-evolution model. The future verification or falsification of this prediction will allow us to qualify the semi-analytic models.


DM haloes from
Millennium Simulation. Ascribed HI and
H2, star formation rates and AGN
properties: provides insufficient FOV for
SKADS benchmark
4x4 deg2 out to z~20 (HI/CO)
~107 objects
star-formation continuum OK

They form part of the SKADS program, which is partly funded by the European Union.
Their purpose is to provide the community with a common testing ground for many of the SKA key
science projects, as well as for instrument design issues on the way to the SKA. Consequently, they
also form an ideal set of simulated skies for SKA pathfinders.

Need the explanation of the simulations!


Step 1: Get the simulations

[get the Radio Continuum Simulations skads_sex.sql.gz data base 103 GB](http://ftp.mpifr-bonn.mpg.de/s-cubed/skads_sex.sql.gz)

[get the HI/CO download the S3SAX01.sql.gz data base 103 GB](http://ftp.mpifr-bonn.mpg.de/s-cubed/S3SAX01.sql.gz)

gunzip skads_sex.sql.gz

Step 2: build a virtual environment via anaconda
install software

matplotlib, astropy, scipy, matplotylib, sqlite

conda create --name SKADS python matplotlib astropy scipy SQLAlchemy

https://github.com/mysql2sqlite/mysql2sqlite

Step 3: access the data base

conda activate SKADS

python
from sqlalchemy import create_engine, text
sqlite_filename = skads_sex.sql'
engine = create_engine('sqlite:///{sqlite_filename}')
with engine.connect() as conn:
  result = conn.execute(text('SELECT * FROM users'))
  for row in results:
    print(row)


Step 4: Generate a plot of sources


