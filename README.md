# Sidekicks

Sidekicks is a repo to keep KB's daily notes.

## Contents

- X01 contamination removal from GRB 190829A (Present - 20200827)

- extracting drzblot X01 spectrum (20200826 - 20200821): We investigated X01 in order to get its 1D spectrum. We found that X01 is a standard star existing in various catalogs. However, only photometry from SDSS DR16 ugriz and 2MASS JHK was available. Then, we decided to directly extract it from 201911 and 202001 G102 images simply because X01 was isolated in a flat background; other images (including 201909, 201910, and 202002 from PID 16042) would be more complicated to extract X01. 20200824/X01_201911_G102_rebkg/* and 20200826/X01_202001_G102/* contain its spectra, while 20200826/X01_together_G102/* contains the combined version. The extraction showed consistency across both epochs and photometry.

Moreover, we preliminary examined 202002 epoch from PID 16042. We cannot locate GRB trace on drzblot images visually. Also, the orientation would cause it to be heavily contaminated. In direct images, a very faint point source was spotted at the GRB location in IR. All drzblot images given X01 were recorded in 20200825.

We also developed hstgrism.headersummary.HeaderSummary. It was added to HSTGRISM 8.3.0a5, and uploaded to PyPI. This class demonstrated in 20200825 that it can simplify the workflow a lot when we added epoch 202002 from PID 16042 to our analysis.

- developing HSTPHOT 1.2.0 (20200820 - 20200818): HSTPHOT 1.2.0 was developed and released to both PyPI and Github. Note: An example in 20200821/01 can be used as demo.

- drzblot/crcorr aperture correction: This computed aperture drzblot/crcorr aperture correction for grism objects. See 20200808 - 20200731. In summary, drzblot/crcorr aperture correction can be as large as ~2% depending on factors such as i) aperture width, ii) trace alignment, iii) background subtraction, iv) filter, and v) drizzle pattern. Recommendation: halfdy >= 4, and performing drzblot/crcorr computation on an isolated star in the FoV.

## Notes

### 20200828
We pursued Method 1 (as discussed in 20200826). (01) presented the workflow to perform contamination removal with an example of removing X01 from GRB190829A at 201909 G102. To achieve this, we added Contamination class to HSTGRISM. This is not a final version yet. We will continue working on this including i) adding the division of 2 for halfdy of the side of contamination, ii) adding the last chunck in 20200828/01 to Contamination (or re-working on the whole structure) to make it a complete flow, iii) working on sanity check.

Andy also suggested to perform non-integer extraction by using aperture correction. For example, if the total aperture width is 10.4 pix, we can take cps value at 9 pix and corrected by apcorr at 10.4 using interpolation.

Also, Andy suggested to perform a simple calculation to see the effect of tilt trace vs non-tilt extraction. He suggested that we should be able to compute the fraction of count in each pixel for non-tilt vs tilt extraction. Use only a couple of x-bin as an example.

### 20200827
We continued trying with Method 2. 20200827/01 was duplicated its introduction from 20200826/04. We completed developing prototype of Method 2. However, testing against GD153 showed that this is a bad approach. We noted that several chucks of code in 20200827/01 can be transferred to performing Method 1.

### 20200826
Today main task was to complete X01 extraction in (01)-(02). We noted that only X01 G102 from 201911 and 202001 were extracted completely. We tried with other epochs but decided not to continue persuing since i) background was not flat in epochs 201909 and 201910 and required special treatment, and ii) epoch 202002 suffered from bad pixels on the blue end of X01 in drzblot image. Although we can go to flt images instead, only epochs 201911 and 202001 should be sufficient since they showed consistency to each other and to photometry. (03) stacked both epochs, and saved to X01_together_G102. We also attached flam_smooth and dateobs columns to the csv output.

We then started to work on details about the contamination removal. Most of the notes were recorded in KB's scrapbook. In (04), we summarized the ideas. We proposed two possible methods. Method 1 simply performs 1D subtraction, while Method 2 requires 2D 'grism_bucket.' We were trying Method 2, when EoD (End of Day) hit. (04) will be carried over to the next day.

Next, we should actually start with Method 1 since it is simpler.

### 20200825

We continued with the aim to extract X01 G102 and G141 from all available images we have. We obtained additional images from PID 16042 at epoch 202002 in both G102 and G141. We diverted our effort to examine this new dataset, and combined it into our current analysis. (01-02) We examined headers of the new files. We i) developed hstgrism.headersummary.HeaderSummary class in order to facilitate this, ii) chose direct-grism pairs, and iii) made ds9 region files for the new images. (03) We generated drzblot images given X01 location. (04) We made trace maps.

Next, we will continue estimating backgrounds, and extracting X01. Then, verify that everything looks consistent. After that, we will perform contamination removal of X01 from GRB 190829A, as this is the main task!

### 20200824

We extracted X01 201911 G102 from its drzblot image. (01) We found issues with background gradient, and trace alignment when extracting X01. Therefore, we discarded this result. We learnt that extraction was likely to be consistent with photometry. (02) We checked SDSS for X01 spectrum. From website with DR16, SDSS has only X01 photometry but not spectrometry. We also made changes to 20200821/01 for SDSS ugriz photometry using DR16 (instead of DR12 from ds9). (03) We tested if we will get better extraction of X01 by manually adjusting trace. Answer was yes. (04) We reworked on background estimation to address the background gradient issue, and also adjusted trace. New output set was recorded in 20200824/X01_201911_G102_rebkg/* (05) X01 201911 G102 was extracted with rebkg set. The result was very good. Halfdy = 3 is recommended. (06) We generated drzblot images of X01 from other epochs including both G102 and G141. 

Next, we will continue estimating backgrounds, and extracting X01. Then, verify that everything looks consistent. After that, we will perform contamination removal of X01 from GRB 190829A, as this is the main task!

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

