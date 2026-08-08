# Workflows and Tools

These open-source repositories address specific microscopy analysis problems
with FIJI/ImageJ macros, Python scripts, GPU-accelerated processing, and Imaris
visualization resources. The descriptions below identify the data context,
main workflow steps, software stack, and intended measurement value.

## Large-Volume Processing and Quantification

<div class="workflow-grid">

<article>
<h3><a href="https://github.com/WeiChenChu/LLSM-Batch-Preprocessing">LLSM Batch Preprocessing</a></h3>
<p><strong>Data</strong><br>Large-volume light-sheet microscopy raw image data.</p>
<p><strong>Workflow</strong><br>Suppress background noise, enhance nuclei signal, and smooth structural boundaries before spot detection or anatomical segmentation.</p>
<p><strong>Stack</strong><br>FIJI/ImageJ macros | GPU-accelerated processing | Imaris</p>
<p><strong>Value</strong><br>Prepares large datasets for more reliable downstream detection, segmentation, visualization, and quantification.</p>
</article>

<article>
<h3><a href="https://github.com/WeiChenChu/yeast-nuclear-puncta-cell-counter">Yeast Nuclear Puncta Cell Counter</a></h3>
<p><strong>Data</strong><br>Yeast fluorescence microscopy images containing nuclear puncta.</p>
<p><strong>Workflow</strong><br>Automate puncta detection and quantitative counting in microscopy images.</p>
<p><strong>Stack</strong><br>Open image analysis pipeline</p>
<p><strong>Value</strong><br>Supports repeatable measurement of nuclear puncta across image datasets.</p>
</article>

</div>

## Dynamics and Colocalization

<div class="workflow-grid">

<article>
<h3><a href="https://github.com/WeiChenChu/TF-Nuclear-Translocation-Analysis">TF Nuclear Translocation Analysis</a></h3>
<p><strong>Data</strong><br>Time-lapse microscopy data with segmented and tracked single cells.</p>
<p><strong>Workflow</strong><br>Refine cell trajectories and quantify stress-induced Dot6-GFP nuclear translocation.</p>
<p><strong>Stack</strong><br>Python | FIJI/ImageJ | TrackMate-Cellpose</p>
<p><strong>Value</strong><br>Connects single-cell motion histories with quantitative transcription factor localization measurements.</p>
</article>

<article>
<h3><a href="https://github.com/WeiChenChu/TIRF_vesicle_colocalize_analysis">TIRF Vesicle Colocalization Analysis</a></h3>
<p><strong>Data</strong><br>Time-series TIRF microscopy images of Glut10 and Rab5 vesicles.</p>
<p><strong>Workflow</strong><br>Detect, identify, and track colocalized vesicles across time.</p>
<p><strong>Stack</strong><br>Python</p>
<p><strong>Value</strong><br>Supports quantitative analysis of vesicle colocalization and dynamics near the cell membrane.</p>
</article>

</div>

## Morphology and Visualization

<div class="workflow-grid workflow-grid--three">

<article>
<h3><a href="https://github.com/WeiChenChu/Cell_Dist_Mesh_Generator">Cell Distance Mesh Generator</a></h3>
<p><strong>Data</strong><br>Microscopy-derived cell positions or regions.</p>
<p><strong>Workflow</strong><br>Generate distance meshes between cells for spatial analysis and visualization.</p>
<p><strong>Stack</strong><br>FIJI/ImageJ macro</p>
<p><strong>Value</strong><br>Makes relative cell spacing available for quantitative visual interpretation.</p>
</article>

<article>
<h3><a href="https://github.com/WeiChenChu/central-nuclei-muscle-analyzer">Central Nuclei Muscle Analyzer</a></h3>
<p><strong>Data</strong><br>Muscle cross-sectional microscopy images.</p>
<p><strong>Workflow</strong><br>Analyze nuclear localization and quantify centrally located nuclei in muscle fibers.</p>
<p><strong>Stack</strong><br>FIJI/ImageJ macro</p>
<p><strong>Value</strong><br>Automates a repeated morphology measurement used in muscle image analysis.</p>
</article>

<article>
<h3><a href="https://github.com/WeiChenChu/IJ_Hot_LUTs_palette">ImageJ Hot LUT Palettes</a></h3>
<p><strong>Data</strong><br>Quantitative microscopy images visualized in Imaris.</p>
<p><strong>Workflow</strong><br>Apply Imaris palette files based on familiar FIJI/ImageJ hot lookup tables.</p>
<p><strong>Stack</strong><br>Imaris palettes</p>
<p><strong>Value</strong><br>Provides reusable, consistent color mapping for microscopy visualization.</p>
</article>

</div>



## Explore the Site

<nav class="section-links" aria-label="Main website sections">
<a href="../home/">
<strong>Home</strong>
<span>Introduction and contact</span>
</a>
<a href="../about/">
<strong>About</strong>
<span>Experience, education, honors, community roles, and profile links.</span>
</a>
<a href="../expertise/">
<strong>Imaging Support</strong>
<span>Microscopy planning, acquisition support, analysis, and reproducible workflow development.</span>
</a>
<a href="../training/">
<strong>Training</strong>
<span>Courses, workshops, recordings, slides, and continuing professional development.</span>
</a>