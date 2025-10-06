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


