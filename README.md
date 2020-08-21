# Sidekicks

Sidekicks is a repo to keep KB's daily notes.

## Contents

- X01 contamination removal from GRB 190829A (Present - 20200821)

- developing HSTPHOT 1.2.0 (20200820 - 20200818): HSTPHOT 1.2.0 was developed and released to both PyPI and Github. Note: An example in 20200821/01 can be used as demo.

- drzblot/crcorr aperture correction: This computed aperture drzblot/crcorr aperture correction for grism objects. See 20200808 - 20200731. In summary, drzblot/crcorr aperture correction can be as large as ~2% depending on factors such as i) aperture width, ii) trace alignment, iii) background subtraction, iv) filter, and v) drizzle pattern. Recommendation: halfdy >= 4, and performing drzblot/crcorr computation on an isolated star in the FoV.

## Notes

### 20200821

We continued with the task to remove X01 contamination from GRB 190829A. (01) We found that X01 is a stable star. (02) We determined that X01 at epochs 201911 and 202001 should be good for subtraction as a template since it lies isolately in a flat background. So, we attempted to extraction it from drzblot image. However, we realized that we need a different drzblot image that is properly flatfielded using X01 location. (03) We performed flatfielded drzblot. And, (04) we completed background estimation of X01 201911 G102 in the new drzblot image, and will be ready for the extraction as the next step.

### 20200820

We continued the main goal that is to perform contamination removal of X01 on GRB 190829A at epoch 201909 and 201910. Given the issues we had, we started by reviewing INS training materials related to photometry (01_INS_training_photometry.ipynb). Then, we developed a short routine to compute photometric equivalence given spectral profile by using pysynphot (02_pysynphot.ipynb) since we would use this routine on our analysis. After that, in 03_hstphot_pipeline_continued.ipynb, we completed HSTPHOT 1.2.0, and tested with GD153 F098M from PID 11552. However, our measurement showed variation upto 0.5 magnitude across three frames. So, we investigated this issue (04_GD153_F098M_highVariation_problem.ipynb). We freshly downloaded drz and flt files from MAST, and performed the same HSTPHOT flow on these data. Problem did not occur. Therefore, we concluded that the problem was dued to bad drizzling 

Next, we can continue with photometry of X01 to verify whether it can be considered as a stable star.

### 20200819

Since we would like to go ahead and try with the GRB 190829A, first thing we would like to check is whether X01 is a stable star by using its photometric property from direct images. To do this, we diverted our effort to developing HSTPHOT, which should help with the productivity in the long run. GD153 F098M from PID 11552 was chosen as an example.

We ended at trying to finish up ApPhot. However, we came across several issues including i) should aperture correction be applied to flt or drz? ii) how to properly compute emag? and iii) we need a code to perform pysynphot of this object as a check. Another issue iv) was also our current measurement of three files (from three locations of GD153 in F098M FoV) provides magnitude varied about 0.5 mag, which does not look correct at all. Although photometric variation across FoV is possible, we would need further investigation on this issue. 

Suggestion is, before trying to resolve those issues, check with INS training library which includes photomery, drizzling, and pysynphot.

### 20200818

Start testing grism emission model. We reviewed ISRs, articles, and other potential sources that would be useful for this effort. We found that Gaussian emission is typically assumed for a grism object given the nature of a point source behaving as a Gaussian. In order to do Gaussian modelling, FWHM would be a key parameter. aXe uses information of a source's shape from input object list (i.e., major axis and minor axis) to compute the equivalence of FWHM. Wayne software uses an analytical form. ISRs show this using SMOV. This task is also the same as simulating a grism object. Therefore, using a simulation software might be the key. However, there is no publicly available software right now: aXeSIM works with python 2 and Wayne is a private project.

### 20200808

- 01: We tested with S04, G141. Results showed negligible drzblot/crcorr < ~1% when halfdy >= 4.
- 02: Tested S04, G102. drzblot/crcorr showed < ~1% when halfdy >= 4.


### 20200807

- 01: We added G141 to HSTGRISM.
- 02: We tested the aperture correction between drzblot and crcorr (similar to what was done in 20200806 and 20200805) with GD153, G141. Results showed that halfdy >= 3 makes the discrepancy negligible at < ~1%.
- 03: We tested similarly with S03 in the field of GRB 190829A, G141, epoch 201911 (proposal ID 15510). Results similarly showed a negligible discrepancy at < ~2% when halfdy >= 4.
- Andy's comment:
 - Present cutout with background subtraction in a larger section, and always put fits file in Dropbox.
 - Try with S04.
 - Try one-image drzblot. We should get essentially no difference between drzblot and crcorr.
 - drzblot/crcorr ratio, make it smoother such as averaging with more x pixels.
 - Check if there is any trend for drzblot/crcorr ratio to be larger with larger wavelength.
 - Can we do better than halfy = 4?
 - Extract cps by using not-full pixel method: i) simply zeroth order, or ii) including first order.
 - Revisit extracting GRB 190829A.
 - Prepare pipeline for image subtraction.
 
 
### 20200806

We performed drzblot/crcorr comparison for the aperture correction with GRB 190829A, G102, 201911XX. S03 and S02 were considered. In general, halfdy >= 4 pixels would bring the discrepancy between drzblot and crcorr to an insignificant level that other factors such as background subtractiona and trace alignment would yield more significant contributions to the discrepancy. Next, we should test with G141.


### 20200805

We performed cps extraction of GD153 for both drzblot and crcorr images in order to demonstrate how significant the aperture correction would be. The results showed that when halfdy >= 2 pixels, G102 drzblot collects approximately equal amounts of cps compared to crcorr. Therefore, the aperture correction is insignificant for this case. What next in this exercise includes i) testing with GRB 190829A or other case with similar dithering pattern, ii) testing with G141.


### 20200804

hstgrism was updated to version 8.1.0 by introducing ObjectMask class. This would facilitate changing aperture width during the computation of aperture correction. What needs to be done next including:
- For GD153, extracting cps from drzblot and four flatcrcorr using aperture width halfdy = 3,4,5, and deriving aperture correction. Then, show that using this aperture correction improves flam from drzblot when compared to calspec.
- Test with GRB 190829A, or find an example that has good dither pattern.


### 20200803

- 01: We continued from 20200731. However, S03 required complicated background subtraction, and we would like to avoid that. Therefore, we tried on a different dataset.
- 02: We tried on GD153 (proposal ID 11552) that has 4-point dither images in the central region. This dataset looked promising. What should be done next was noted in the document. Also, note that this set that has POSTARGs around -20,0 which is still off by hundreds of pixels compared to GRB data of which POSTARG2 around 0,0. Therefore, after showing this GD153 set as a proof of concepts, we (might) still need a different dataset that would be more suitable to our original problem.


### 20200731

We would like to compute the aperture correction for HST grism extraction when performing on a drz-blot flt frame. The day ends with creating ./drzblot_S03/idlk01jmq_flt.fits, which will be used in the next step. However, code check must be performed before proceeding.

