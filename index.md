
# Tuesday Oct 20 2020

1. LEO I
   Need to adress reviewer comments.
   Add plot of the NFW profile to prove it's not enough.
2. LIGHETR
   - Should implement black body analysis.
   - Should do the analytical form for the los alamos people.
3. GWEMLISA
   Gotta start populating the draft.
4. SPIN PREC
   q8-chi01 is in Ecc1.
   Should I start more?

# Tuesday Oct 13 2020

1. GWEMLISA
   * Added vel params on binary class.
   * Gotta start populating the draft.
2. LIGHETR
   - Should implement black body analysis.
   - Should do the analytical form for the los alamos people.
3. LEO I
   * Need to adress reviewer comments.
   * Add plot of the NFW profile to proof it's not enough.
4. SPIN PREC
   * Get account on stampede and start runs.
5. BROWN DWARF
    * Ter cara de pau...
6. LIGO
    * SCI SUM
        Finish the last comments.
    * Catalog
        Change revision number.

# Tuesday May 05 2020
Testing MathJax: 1234 $\alpha$

# Friday May 01 2020

1. GWEMLISA
   Waiting on Greg Ashton.
2. LIGHETR
   Got cubes for one night, now waiting on astrometry.
   Created [flow diagram](https://app.diagrams.net/#G1xkEnxAPcQWNWI-WOYh2MEoruqBJofno9) .
3. LEO I
   Fixing plots. Confidence plots now show the median.
4. SPIN PREC
   ?
5. BROWN DWARF
   Not diving into this yet.
6. LIGO
    * SCI SUM
       Waiting for comments from Cody. Editorial team has not read it yet
    * ROTA
      Looks like it's taken care of.

# Thursday April 30 2020

## PROJECTS

1. GWEMLISA
Waiting on Greg Ashton.
2. LIGHETR
Waiting on Greg Zeiman.
3. LEO I
Waiting on reruns.
4. SPIN PREC
?
5. BROWN DWARF
Not diving into this yet.
6. LIGO
    * SCI SUM
    Waiting for comments.
    * ROTA
    Idk where we are in this.


# Tueday December 3 2019

DIAGNOSIS

Added clear sky chart to email.


# Tuesday November 26 2019

LEO I

Ran mkherm in new tidal values Karl sent over email (Had to find and recompile mkherm... Where is the prior one??). The tidal values are in the file dispersion_Nov21.txt, under the following folder structure in wrangler:

```bash
cd $WORK/leo/mkherm_testground/
make -f mkherm.f
mkdir tidal1
mkdir tidal2
```
In order to make the input file for mkherm I multiplied columns 4 and 5 (for the two tidal radii) by the sigma and sigma-diff from the paper:

```python
import numpy as np
d=np.loadtxt("dispersion_Nov21.txt")
aa=np.zeros((len(d),11))
for bin in d:
    aa[:,0]=d[:,0];
    aa[:,3]=d[:,1]*d[:,5]
    aa[:,4]=(d[:,3]-d[:,1])*d[:,5]
np.savetxt("tidal2/SIGtidal2.txt",aa,fmt="%.3f")
aa=np.zeros((len(d),11))
for bin in d:
    aa[:,0]=d[:,0];
    aa[:,3]=d[:,1]*d[:,4]
    aa[:,4]=(d[:,3]-d[:,1])*d[:,4]
np.savetxt("tidal1/SIGtidal1.txt",aa,fmt="%.3f")
```
Then I ran mkherm on this files, tarred the result and sent it to Karl. Waiting for his reply to run the models.

Lambda_reweight script

Got an email from Wolgang saying they are using the posteriors to modify the priors on my script, which is nonsense. Gotta read the paper and his paper carefully now.


# Friday November 15 2019

Updated Diagnosis.py to make sure everything runs smoothly.
Now it includes the time of the event in the email.

# Tuesday July 23 2019

Edited the makegrid_all.py to just have the 0 mass bh runs. It uses makegrid_all and jobsplitter, created after a script karl linked me too.

```bash
$ cd /work/03237/majoburo/wrangler/leo/slurms0.0_4
$ python makegrid_all.py
$ ~/jobsplitter2w run0.0_4 20 6  "24:00:00"
$ for i in {1..3}; do sbatch run0.0_4_$i.slurm; done
```

Work place for Karl on Leo I's project is:
```
$ cd /work/00115/gebhardt/maverick/leo/hoku/leo/mateo
```

His binning is under the run0 file.

```
  7 awk '{if($5<178) print $0}' mateo.use > mb0c
  8 awk '{if($5>178&&$5<223) print $0}' mateo.use > mb1c
  9 awk '{if($5>223&&$5<278) print $0}' mateo.use > mb2c
 10 awk '{if($5>278&&$5<347) print $0}' mateo.use > mb3c
 11 awk '{if($5>347&&$5<432) print $0}' mateo.use > mb4c
 12 awk '{if($5>432&&$5<667) print $0}' mateo.use > mb5c
 13 awk '{if($5>347&&$5<667) print $0}' mateo.use > mb6c
```

For the tidal bins, I'm separating them at 432 and 347 (400?). the separations of our most outer bins (I can also the 400 limit, as the paper suggests, in which case there might have to be an extra bin made). I need to remember how to create the light profile in the format for karl's code..
```
$ cd /work/03237/majoburo/wrangler/leo
$ python tidalmod.py --sb extsbLeoI.tab --sig newdata.dat 430 400
```

For whatever reason bin_r.out in base and bin_r.out in the actual output files for each model are very different... But I trust the one in the output files since this an output file.
Use SIG?.txt and SB?.txt for the sb profile and the dispersion profile.
Need to figure out how to make an ?.in file for the sb profile.

