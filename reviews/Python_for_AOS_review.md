# Reviews

## Atmos Ocean Launch

URL: [Data carpentry blog](https://datacarpentry.org/blog/2018/09/atmos-ocean-launch) <BR>
Suggested URL: [Carpentries Lab AOS Lesson](https://carpentrieslab.github.io/python-aos-lesson/) <BR>
Reviewer: Rob Fatland <BR>
Review Summary: Awesome!  <BR>
Context: [Data Carpentry](datacarpentry.org); specifically self-learning of ocean/atmosphere Python data science tools <BR>
Author: [Damien Irving](https://drclimate.wordpress.com/who-is-dr-climate/) <BR>
Open in Binder: No <BR>
Pangeo-sympatico: Need an env with cmocean installed


* From the blog it takes a bit of care to navigate a diaspora of links; 
for example [the github link](https://github.com/carpentrieslab/python-aos-lesson) provides a 
[DC link](https://carpentrieslab.github.io/python-aos-lesson/)
above a bunch of AMOS event links... perhaps place the DC link in the p-d/e-m table?
* The *PyAOS Stack* page has a nice wrap-up on *Navigating the Stack*. For the impatient person it could 
possibly benefit from a Don't Panic message at the top as well; one that includes a shorter version of this. 
'The main takeaway is a strategy: Start with `GeoViews` and work examples to bring the other elements of 
the stack into focus.' ...or something along those lines that aligns with the workshop.
* Suggest where `miniconda` will / will not be better than working with `conda`.
* pangeo JHub does not seem to have `cmocean` installed; lesson has an excellent remark on `conda create` environments.


```
conda create -n pyaos-lesson jupyter xarray netCDF4 cartopy cmocean
conda activate pyaos-lesson
```

