# CIEDE2000 color difference formula in AWK

This page presents the CIEDE2000 color difference, implemented in the AWK programming language.

![Logo for CIEDE2000 in AWK](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## Our CIEDE2000 offer

This production-ready file, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.awk](./ciede2000.awk)|`number`|64|General|Interoperability|

### Software Versions

- macOS 26
- Ubuntu 24
- GNU Awk 5.2.1
- Mawk 1.3.4

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```awk
# Example of two L*a*b* colors
l1=93.9 a1=125.4 b1=-7.6
l2=98.1 a2=60.4  b2=3.9

printf "$l1,$a1,$b1,$l2,$a2,$b2" | awk -f ciede2000.awk
# ΔE2000 = 13.35496927007265

# Example of parametric factors used in the textile industry
kl=2.0 kc=1.0 kh=1.0

# Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
printf "$l1,$a1,$b1,$l2,$a2,$b2,$kl,$kc,$kh" | awk -f ciede2000.awk --canonical
# ΔE2000 = 13.17969195699573
```

You may use the command `awk -f ciede2000.awk < file.csv` to evaluate color differences in a CSV batch.

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

```
CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.83453294874678
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 747.23 seconds
     Average Delta E : 67.13
   Average Deviation : 7.4e-15
   Maximum Deviation : 2e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.8343428812861
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 746.57 seconds
     Average Delta E : 67.13
   Average Deviation : 7.7e-15
   Maximum Deviation : 2e-13
```

## Public Domain Licence

You are free to use these files, even for commercial purposes.
