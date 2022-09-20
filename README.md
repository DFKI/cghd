# Circuit Graph Hand-Drawn (CGHD)
This repostitory contains images of hand-drawn electrical circuit diagrams as well as accompanying annotation and segmentation ground-truth files.

## Structure
The folder structure is made up as follows:

```
cghd
│   classes.json
└───drafter_D
│   └───annotations
│   │   │   CX_DY_PZ.xml
│   │   │   ...
│   │
│   └───images
│   │   │   CX_DY_PZ.jpg
│   │   │   ...
│   │
│   └───segmentation
│   │   │   CX_DY_PZ.jpg
│   │   │   ...
│
│   LICENSE
│   README.md
```

Where:

 - `D` is the (globally) running number of a drafter
 - `X` is the (globally) running number of the circuit (12 Circuits per Drafter)
 - `Y` is the Local Number of the circuit's Drawings (2 Drawings per Circuit)
 - `Z` is the Local Number of the Drawings's Image (4 Pictures per Drawing)

### Image Files
Every image is RGB-colored and stored as either `jpg` or `jpeg`.

### Bounding Box Annotations
A complete list of class labels including a suggested mapping table to integer numbers can be found in `classes.json`. The annotations contain bounding boxes of contained symbols and are stored in the [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) format.

### Segmentation Maps
Segmentation images are available for some samples and bear the same resolution as the respective image files. They are considered to contain only black and white pixels indicating areas of drawings strokes and background respectively.

### Netlists
For some images, there are also netlist files available, which are stored in the [ASC](http://ltwiki.org/LTspiceHelp/LTspiceHelp/Spice_Netlist.htm) format.

## Current state
The dataset ist still beeing extended and this repository is currently under construction. If you are interested in this domain and would like to contribute, please write an email to: johannes.bayer@dfki.de

## Citation

If you use this dataset for scientific publications, please consider citing us as follows:

```
@inproceedings{thoma2021public,
  title={A Public Ground-Truth Dataset for Handwritten Circuit Diagram Images},
  author={Thoma, Felix and Bayer, Johannes and Li, Yakun and Dengel, Andreas},
  booktitle={International Conference on Document Analysis and Recognition},
  pages={20--27},
  year={2021},
  organization={Springer}
}
```

## Guidelines
These guidelines are used throughout the generation of the dataset. They can be used as an instruction for participants and data providers.

### Drafter Guidelines
 - 12 Circuits should be drawn, each of them twice (24 drawings in total)
 - Most important: The drawing should be as natural to the drafter as possible
 - Free-Hand sketches are preferred, using rulers and drawing Template stencils should be avoided unless it appears unnatural to the drafter
 - Different types of pens/pencils should be used for different drawings
 - Different kinds of (colored, structured, ruled, lined) paper should be used
 - One symbol set (european/american) should be used throughout one drawing (consistency)
 - It is recommended to use the symbol set that the drafter is most familiar with

### Image Capturing Guidelines
 - For each drawing, 4 images should be taken (96 images in total per drafter)
 - Angle should vary
 - Lighing should vary
 - Moderate (e.g. motion) blur is allowed
 - All circuit-related apsects of the drawing must be _human-recognicable_
 - The drawing should be the main part of the image, but _naturally_ occuring objects from the environment are welcomed
 - The first image should be _clean_, i.e. ideal capturing conditions
 - Kinks and Buckling can be applied to the drawing between individual image capturing

### Object Anotation Guidelines
 - General Placement
   - A symbol should be __completely__ surrounded by its box
   - Boxes should be as tight as possible to the symbol
   - In case of connecting lines not completely touching the symbol, the bounding box should extended (only by a small margin) to enclose those gaps (epecially considering junctions)
 - Annotations of subcomponents should be avoided (e.g. LED of an optocoupler)
 - **Junction** annotations 
   - Used for both actual junction points and wire line corners
   - Should not be used for corners or junctions that are part of the symbol definition (e.g. Transistors)
 - **Text** annotations
   - Semmantically meaningful chunks of information
     - component characteristics enclosed in a single annotation (e.g. __100Ohms__, __10%__ tolerance, __5V__ max voltage)
     - Component Terminal Labels
     - Individual Lines in text blocks
   - Texts not related to the Circuit should be ignored (e.g. Brief paper, Company Logos)
   - Characters which are part of the Symbol Definition should not be annotated (e.g. Schmitt Trigger __S__, and gate __&__, motor __M__, Polarized capacitor __+__)
     - Only add text annotation if they indicate non-standard terminals

### Segmentation Map Guidelines
 - Areas of __Intended__ drawing strokes (ink and pencil abrasion respectively) should be marked black, all other pixels (background) should be white
 - shining through the paper (from the rear side or other sheets) should be considered background
