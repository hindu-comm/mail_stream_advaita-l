+++
title = "145 Anand Hudli"
date = "1998-06-25"
upstream_url = "https://lists.advaita-vedanta.org/archives/advaita-l/1998-June/008987.html"

+++
[Archive link](https://lists.advaita-vedanta.org/archives/advaita-l/1998-June/008987.html)

 Knowing the tithi or lunar day is important for many occassions. For
 example, the Rama Navami falls on the ninth lunar day of the month
 of Chaitra. To know the tithi at any given time, we may make use
 of the information in the panchanga. Most panchanga's list the
 ending times of tithi's during the entire calendar year. But these
 times are in IST (Indian Standard Time) for panchangas prepared in
 India. So the first step is to convert the IST ending times for the
 relevant dates to times in the local time zone.

 For example, let us say the panchanga lists the ending time of the
 dashamI tithi (10th tithi) as 7:00 AM (IST) on April 25 and the
 ending time of the ekAdashI tithi (11th tithi) as 8:30 AM on April
 26th. What is the tithi at 6:00 AM in New York on April 25?

 1) First convert the ending times to Eastern Daylight Savings Time
    (EDT), because that is the time followed in New York for April
    25. EDT is 9 hours 30 minutes behind IST. So the ending time
    of the dashamI becomes 9:30 PM EDT, April 24, and that of the
    ekAdashI becomes 11:00 PM EDT, April 25.

 2) From 1) it is clear that the ekadashI begins at 9:30 PM EDT on
    April 24 and prevails until 11:00 PM EDT, April 25. Therefore,
    the tithi at 6:00 AM in New York on April 25 is ekAdashI.


 What to do if the panchanga is not available
 --------------------------------------------

 In this case, you have to have access to at least an ephemeris (such
 as the Nautical Almanac or the Astronomical Ephemeris) which lists
 the celestial longitudes of (among other bodies) the Sun and the
 Moon. These ephemerides are available in many libraries in the US and
 elsewhere.

 Such ephemerides usually list the longitudes on a daily basis
 for Midnight GMT. In order to find the tithi at a given place at a
 given local time, we can first convert the local time to GMT and find
 the preceding midnight GMT and the succeeding midnight GMT. Then by
 simple interpolation, we can find the longitudes of the Sun and the
 Moon at the specified time and  compute the tithi.

 Let S_1 = longitude of the Sun at the preceding midnight GMT
     S_2 = longitude of the Sun at the succeeding midnight GMT
     M_1 = longitude of the Moon at the preceding midnight GMT
     M_2 = longitude of the Moon at the succeeding midnight GMT

 Let T = time at which the tithi is required in GMT, and expressed
         as a fraction of a day (for example, 12 noon GMT will be
         0.5, 6 AM GMT will be 0.25, 6 PM GMT will 0.75, etc.)

 Then the mean rate of the Sun's movement, r_S = (S_2 - S_1)
      the mean rate of the Moon's movement, r_M = (M_2 - M_1)

 (Here, by Sun's movement I only mean the apparent movement of the
  Sun in the zodiac. Since observations are from the earth, it is
  convenient to imagine that the Sun, Moon and planets move in the
  zodiac with respect to the observer on earth.)

  The longitude of the Sun at time T, (say) S = S_1 + (r_S * T)
  The longitude of the Moon at time T, (say) M = M_1 + (r_M * T)

 (These longitudes are approximate because we assumed the motion of
 the Sun and Moon is with constant speed. But this is not true in
 reality. The simple interpolation scheme will work in many cases,
 but for more accuracy, we need to compute the positions of Sun and
 Moon, without resorting to such interpolation. To do this we must
 have access to formulae from celestial mechanics. There are computer
 programs which do this kind of calculations.)

 Once S and M are known, the tithi can be found by calculating
 (((360 + M - S) mod 360)/12) + 1.

 Example: Suppose we want to find the tithi at 8:00 AM in New York
 on April 25. This time T in EDT will be 12 Noon GMT (EDT is 4 hours
 behind Greenwich Mean Time, GMT). Suppose the ephemeris lists the
 longitudes of the Sun as 20 degrees 30 minutes 0 seconds on April
 25 at Midnight GMT and 21 degrees 30 minutes 0 seconds on April
 26 at Midnight GMT, and the longitudes for the Moon as 140 degrees
 10 minutes 0 secs on April 25 at Midnight GMT and 152 degrees 50
 minutes 0 secs on April 26 at Midnight GMT.

 Mean rate of Sun's motion = 21 degrees 30 mins - 20 degrees 30 mins
                           = 1 degree 0 mins 0 secs/day

 Mean rate of Moon's motion= 152 degrees 50 mins - 140 degrees 10 mins
                           = 12 degrees 40 mins 0 secs/day

 Given time T, at which tithi is required,
 expressed as fraction of a day = 12 hours/ 24 hours
                                       = 0.5 day

 So longitude of Sun, S at time T = 20 deg 30 mins +
                                    (1 deg/day * 0.5 day)
                                  = 20 deg 30 mins + 30 mins
                                  = 21 degrees 0 mins

 The longitude of the Moon, M at time T = 140 deg 10 mins  +
                                        (12 deg 40 mins/day * 0.5 day)
                                        =  140 deg 10 mins +
                                           6 deg 20 mins
                                        =  146 deg 30 mins

 Once we have the longitudes of the Sun and the Moon at the given
 time, we can find the tithi.

 tithi = (((360 + M - S) mod 360)/12) + 1
       = (((360 + 146 deg 30 mins - 21 deg 0 mins) mod 360)/12) + 1
       = (((360 + 125 deg 30 mins) mod 360)/12) + 1
       = ((485 deg 30 mins mod 360 deg)/12) + 1
       = (125 deg 30 mins)/12 deg + 1
       = 10 + 1 = 11 ( Here the division is only integer division,
                       in which the remainder is neglected)

 The tithi value of 11 indicates that it is the shukla pakSha
 ekAdashI, ie. the 11th lunar day in the bright half of the month.

 Note: The longitudes found in the ephemerides I mentioned are
 actually with respect to the moving equinoxes. The Hindu calendar
 system considers the longitudes with respect to fixed equinoxes.
 Such a system is called nirayana. The moving equinoxes system is
 called sAyana. The nirayana longitude of a celestial body differs
 from its sAyana longitude by a factor called AyanAMsha. Since the
 this AyanAMsha cancels out when we subtract the longitude of the
 Sun from the Moon, the tithi calculation as outlined above will
 still be correct. But in the calculation of nakShatra (asterism) at
 a given time, only the longitude of the Moon is involved. So in that
 case, we will have to consider the AyanAMsha and subtract it from the
 longitude of the Moon, before proceeding with the calculation.

  I will write more about nakShatra calculation later.

 Anand








______________________________________________________
Get Your Private, Free Email at http://www.hotmail.com

