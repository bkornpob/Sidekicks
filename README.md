# Sidekicks

Sidekicks is a repo to keep KB's daily notes.

## Notes

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

