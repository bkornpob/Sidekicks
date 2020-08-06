# Sidekicks

Sidekicks is a repo to keep KB's daily notes.

## Notes

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

