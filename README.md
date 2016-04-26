#SWMMIO

SWMMIO is a set of python tools for interacting with and visualizing results from EPA Stormwater Management Model input and output files (.inp and .rpt). These tools are being developed specifically for the application of flood risk management.


### Prerequisites
SWMMIO functions by processing .inp and .rpt (input and report) files produced by EPA SWMM5. In order for these tools for work properly, an associated pair of .inp and .rpt files should be located within the same directory. SWMMIO (I think) relies only on pre-installed Python 2.7 libraries. Images2Gif was copied within this project and one line was edited to work herein (I need to dig to remember which). 

###Usage:


In IDLE, add the directory holding the SWMMIO python scripts to your sys.path variable and import the modules:
```
import sys
sys.path.append('/path/to/swmmio/directory')
import swmmio
import swmm_graphics as sg
import swmm_utils as su
import swmm_compare as scomp

```
Instantiate  some model objects by pointing SWMMIO to a directory containing a model's .inp and .rpt files:
```
model_a = swmmio.model('/directory containing .inp and .rpt files')
model_b = swmmio.model('/other directory containing .inp and .rpt files')
```

Create an image (.png) visualization of the model. By default, pipe stress and node flood duration is visualized. 
Many options can be passed to control how and what data is visualized.
```
sg.drawModel("FileName", model_a)
```

Create an animated gif of a model's response to a storm. Again many options can be passed.
```
sg.animateModel("AnimationFileName", model_a, 
				startDtime='JAN-01-1990 11:59:00', 
				endDtime='JAN-01-1990 12:01:00')
```

Generate a comparison report showing changes in node flooding between two models. Presumably, the models
will represent a baseline model compared to a flood mitigation alternative.
``` 
scomp.comparisonReport(model_a, model_b)
```

Create visualization of the impact of a given alternative with respect to the baseline conditions.
```
scomp.drawModelComparison("imageFileName", model_a, model_b, options={'conduitSymb':'compare_hgl'})
```

Exporting data for further processing
```
model_a.exportData() #csv table of results data for each node (flood duration, hgl, etc)
model_a.exportData(type='conduit') #csv table of results data for each conduit

``` 

### Acknowledgments
For use in generating animations of SWMM models, thanks to [images2gif.py](https://gist.github.com/jonschoning/7216290)
