###################
Summary of TMA tests
###################
.. note::

   **This technote is a work-in-progress.**
.. abstract::
   This technote is linked with: https://rubinobs.atlassian.net/browse/SITCOM-1254

   This technote sumamrises the tests (both past and ongoing) verifcation tests carried out with different operation al components of the TMA. With the analysis still in progress we are expected to derive conclusive behaviour of the TMA and populate this technote with summary of each tests, inferences, and proposed next steps.

   This technote also serves as an index to the other tech notes produced on each test or data analysis
   for TMA performace.

Introduction
============

Most of the performance analysis is based on the data from 1-3 nights in the second half of March 2023, except for the slew analysis  which also included the data taken since November 2022.

TMA Performance Analysis
====================================

Pointing verification
---------------------

* The current pointing model gives an error ~ 10 arcsec (still in development)

* Based on data limited to two nights, variation was presented in relative pointing for RA -- in both forward- and backward-commanded pointing -- spanning the range of -100< :math:`{\Delta}RA` < 100 arcsec.

* `SITCOMTN 077`_ The drift during tracking was analysed on data of 1 night and was observed to be of order of :math:`10^{-4}`  arcsec for both RA and Dec. The average drift velocities  for both RA and Dec were similar in magnitude but different in directions. The average angular drift velocity (0.6 arcsec/min) is within 1sigma of the expected. Hence, from this dataset we conclude a drift behavior of the tracking within normal expectations.

.. _SITCOMTN 077: https://sitcomtn-077.lsst.io

* `SITCOMTN 063`_, `SITCOMTN 065`_ Under a 3.5 degree random offset, it was clear that the pointing model (for a test position set 1039 to 1071) progressively degraded with time with an average offset rate of 0.55 arcsec /min. Correcting for this rate, we get an on-sky precision (1 :math:`{\sigma}`) of 0.3 arcsec for RA and 0.21 arcsec for Dec. This is close enough to the required 0.2 arcsec precision.
.. _SITCOMTN 063: https://sitcomtn-063.lsst.io
.. _SITCOMTN 065: https://sitcomtn-065.lsst.io


TMA jitter verification
----------------------




Slew and settle verification
----------------------------

* `SITCOMTN 067`_, `SITCOMTN 068`_ The velocity, acceleration and jerk of TMA was analysed under 3.5 degree random slews. Using a methodology that involved identifying the slew profiles, and using spline interpolation, it was determined all the slew profiles met the specifications without hitting the maximum permissible design limits. It was also noted that majority of the flagged/extreme slews could be corrected through a smoothing algorithm applied to the motion profiles to account for plausible noise introduced by the encoder (which prevented obtaining accurate slew profiles originally). Furthermore,  slew and settle requirements for 3.5 degree slews with elevation less than 60 degrees are met 96% of the time. The failures tend to occur at times with larger slews in elevation relative to azimuth.
.. _SITCOMTN 067: https://sitcomtn-067.lsst.io
.. _SITCOMTN 068: https://sitcomtn-068.lsst.io

StarTracker
------------
* `SITCOMTN 064`_ Startracker: star trails-centre finder
.. _SITCOMTN 064: https://sitcomtn-064.lsst.io
* `SITCOMTN 071`_ The current pinting pointig model devloped for TMA uses the narrow camera. The offset from the narrow camera to the fast camera is calculated and verified, such that when the TMA is pointed at an object, it will be positioned at the boresight of the narrow camera, and then introduce a known offset to put the object in the field of view of the narrow camera. It was found that to center the object in the fast camera, we should slew to the object and then apply the following command: mtcs.offset_azel(az=-208, el=508). However, it was also found empirically on multiple nights that the sign of the az offset was incorrect, and the command mtcs.offset_azel(az=208, el=508) successfully put the object in the fast camera field of view, although not always centered.
.. _SITCOMTN 071: https://sitcomtn-071.lsst.io

Others
-----

* `SITCOMTN 066`_ We have not resolved encoder disagreement events that have been noted in data from 2023. More data and detailed analysis is required to understand patterns and potential cause of such disagreements.
.. _SITCOMTN 066: https://sitcomtn-066.lsst.io

* `SITCOMTN 080`_ Torque hysteresis was also observed during the first TMA balancing post addition of MAM3 cell - this behaviour was observed at a minimal of 1% of maximum speed and at a very specific elevation angles of < 3.85 degrees. A detailed data analysis of of historical slews identified this behaviour to be present since before the first TMA balancing. A similar elevation torque anomaly also occurs at zenith. The possible causes for such strain in required torque (or drag) are linked to missing elevation structure magnets in the  axis motor, disabled elevation drives (2 at the time of observations), elevation breaks and elevation axis hard stops.
.. _SITCOMTN 080: https://sitcomtn-080.lsst.io

Index of analyses in progress
=============================
* `SITCOM_704`_ - First pointing model generation-Data acquisition preparation
.. _SITCOM_704: https://jira.lsstcorp.org/browse/SITCOM-704

* `SITCOM_706`_ - Relative pointing verification
.. _SITCOM_706: https://jira.lsstcorp.org/browse/SITCOM-706

* `SITCOM_708`_, `SITCOM_1173`_ - TMA jitter verification
.. _SITCOM_708: https://jira.lsstcorp.org/browse/SITCOM-708
.. _SITCOM_1173: https://jira.lsstcorp.org/browse/SITCOM-1173

Related documents
================

For all the tests, the requirements for TMA are extracted from <link>
