# Large timescales and time values # {#timescale-constraints}

[[ECMASCRIPT]] is unable to accurately represent numeric values greater than 2<sup>53</sup> (`9007199254740991`) using built-in types. Therefore, interoperable services cannot use such values.

All timescales are start times used in a DASH presentations SHALL be sufficiently small that no timecode value exceeding 2<sup>53</sup> will be encountered, even during the publishing of long-lasting live services.

Note: This may require the use of 64-bit fields, although the values must still be limited to under 2<sup>53</sup>.

<div class="example">

The issue does not arise with the common 90 KHz [=timescale=]. Counting time since the Unix epoch until 11 November 2019 we get `141721093260000` which is well within the allowed range of values.

Another common timescale is 10000000 (10 million [=timescale units=] per second) often used by Smooth Streaming. Counting time since the Unix epoch until 11 November 2019 we get `15746788140000000` which does exceed the critical value and will result in broken playback on many clients! To correct such an error, use a smaller timescale or a [=MPD timeline=] zero point that is not so far in the past.

</div>

# Representing durations in XML # {#xml-duration-constraints}

All units expressed in [=MPD=] fields of datatype `xs:duration` SHALL be treated as fixed size:

* 60S = 1M (minute)
* 60M = 1H
* 24H = 1D
* 30D = 1M (month)
* 12M = 1Y

[=MPD=] fields having datatype `xs:duration` SHALL NOT use the year and month units and SHOULD be expressed as a count of seconds, without using any of the larger units.