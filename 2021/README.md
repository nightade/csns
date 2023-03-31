# 2021 Reproducing [Louf 2013](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.111.198702) - Dataset Description
## 🛑 To make it more usable...
- include ZCTA ↔ State/County ↔ ZIP mapping data

## 1. gaz_zcta : Area Data (2000, 2010-2016)
**Zip Code Tabulate Areas** ... [more](https://www.census.gov/programs-surveys/geography/guidance/geo-areas/zctas.html)
<br>From US census bureau **Gazetteer Files** ... [more](https://www.census.gov/geographies/reference-files/time-series/geo/gazetteer-files.1990.html)
<br>ZCTA and ZIP differ in areas & codes [more](https://udsmapper.org/zip-code-to-zcta-crosswalk/)
<br>💬 <span style="background-color:gold">Note1</span> : Datasets in this very repo is **highly reduced** (by me), so take a look at the [Full Layout](https://www.census.gov/programs-surveys/geography/technical-documentation/records-layout/2010-zcta-record-layout.html)
<br>... excluded columns are mostly 1) <u>calculated values</u> that depends on other columns e.g. percentage
<br>... or 2) same data <u>from different sources</u>
<br>💬 <span style="background-color:gold">Note2</span> : Gazetteer files are available for only 1990, 2000, 2010~
<br>... whose **columns are slightly different** due to the changes related to collection
<br>... (especially, 2010 dataset lacks over half the columns of the other sets)
<br>
- 📘 **Major columns**
    - GEOID : ZCTA census code
    - POP : population
    - HU : housing unit
    - ALAND : area land in square-meterf
    - STATE : state name (2 letter abbrev.)
- 📘 **Misc. columns**
    - AWATER : area water in square-meter
    - (...)_SQMI : in square-mile
    - INTPTLAT, INTPTLONG : Internal Point Latitude, Longitude

## 2. dat : Density of Employment (1999-2016)
Integration of area data(←gaz_zcta) and **employment data(←ZIP Codes Business Patterns)** [ZBP](https://www.census.gov/data/developers/data-sets/cbp-nonemp-zbp/zbp-api.html)
<br>...which is processed in *empirical_write.ipynb*
<br>💬 <span style="background-color:gold">Note1</span> : \#Employment is about *ZIP* area, whereas area data is about *ZCTA* area.ZC
<br>... ZIP and ZCTA do not perfectly align, but I suppose they match **well enough** to observe the scaling properties ... [more](https://udsmapper.org/zip-code-to-zcta-crosswalk/)
<br>💬 <span style="background-color:gold">Note2</span> : Density of Employment $\rho$ equals (EMP)÷(gaz_zcta.ALAND)
<br>... for the 2001-2005 EMP is applied 2000 ALAND, and 2010 ALAND for the 2006-2009
- **Columns**
    - GEO_TTL : name of the zip area from ZBP API
    - GEOID : area key from gaz_zcta
    - EMP : \#Employment
    - ZIP : ZIP code
    - index_gaz : row index in gaz_zcta
    - rho : Density of Employment [/m²]

## ykp : Year-\#Subcenter($k$)-Population ($\alpha$=5,10,20)
See SI of the paper