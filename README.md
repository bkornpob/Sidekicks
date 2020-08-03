# Sidekicks

Sidekicks is a repo to keep KB's daily notes.

## Notes

### 20200731

We would like to compute the aperture correction for HST grism extraction when performing on a drz-blot flt frame. The day ends with creating ./drzblot_S03/idlk01jmq_flt.fits, which will be used in the next step. However, code check must be performed before proceeding.

### 20200803

- 01: We continued from 20200731. However, S03 required complicated background subtraction, and we would like to avoid that. Therefore, we tried on a different dataset.
- 02: We tried on GD153 (proposal ID 11552) that has 4-point dither images in the central region. This dataset looked promising. What should be done next was noted in the document. Also, note that this set that has POSTARGs around -20,0 which is still off by hundreds of pixels compared to GRB data of which POSTARG2 around 0,0. Therefore, after showing this GD153 set as a proof of concepts, we (might) still need a different dataset that would be more suitable to our original problem.
