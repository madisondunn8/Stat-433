hw1
================
Madison Dunn
9/16/2021

Github link: <https://github.com/madisondunn8/Stat-433>

``` r
library("readr")
```

    ## Warning: package 'readr' was built under R version 4.0.5

``` r
library("ggplot2")
library("dplyr")
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
bridges = read_csv("WI20.csv")
```

    ## Rows: 14271 Columns: 123

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (49): STRUCTURE_NUMBER_008, ROUTE_NUMBER_005D, HIGHWAY_DISTRICT_002, COU...
    ## dbl (72): STATE_CODE_001, RECORD_TYPE_005A, ROUTE_PREFIX_005B, SERVICE_LEVEL...
    ## lgl  (2): CRITICAL_FACILITY_006B, TEMP_STRUCTURE_103

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
str(bridges)
```

    ## spec_tbl_df [14,271 x 123] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ STATE_CODE_001         : num [1:14271] 55 55 55 55 55 55 55 55 55 55 ...
    ##  $ STRUCTURE_NUMBER_008   : chr [1:14271] "00000000000F303" "00000000000F304" "00000000000F310" "00000000000F311" ...
    ##  $ RECORD_TYPE_005A       : num [1:14271] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ ROUTE_PREFIX_005B      : num [1:14271] 6 6 6 6 6 6 6 6 6 6 ...
    ##  $ SERVICE_LEVEL_005C     : num [1:14271] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ ROUTE_NUMBER_005D      : chr [1:14271] "00010" "01015" "00024" "00021" ...
    ##  $ DIRECTION_005E         : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ HIGHWAY_DISTRICT_002   : chr [1:14271] "07" "07" "06" "03" ...
    ##  $ COUNTY_CODE_003        : chr [1:14271] "051" "051" "115" "115" ...
    ##  $ PLACE_CODE_004         : chr [1:14271] "00000" "00000" "00000" "00000" ...
    ##  $ FEATURES_DESC_006A     : chr [1:14271] "'FLAMBEAU BEAR RIVER'" "'TROUT RIVER'" "'WEST BRANCH RED RIVER'" "'RED  RIVER'" ...
    ##  $ CRITICAL_FACILITY_006B : logi [1:14271] NA NA NA NA NA NA ...
    ##  $ FACILITY_CARRIED_007   : chr [1:14271] "'IRR BIA RTE 10'" "'IRR ROUTE 15'" "'IRR BIA RTE  24'" "'IRR BIA RTE  21'" ...
    ##  $ LOCATION_009           : chr [1:14271] "'6KM NW OF LAC DU FLAMBEAU'" "'LAC DU FLAMBEAU'" "'10 KM  NE  OF  BOWLER'" "'13 KM  NE  OF  BOWLER'" ...
    ##  $ MIN_VERT_CLR_010       : num [1:14271] 100 100 100 100 100 ...
    ##  $ KILOPOINT_011          : num [1:14271] 0.161 1.5 2.737 8.372 3.22 ...
    ##  $ BASE_HWY_NETWORK_012   : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ LRS_INV_ROUTE_013A     : chr [1:14271] "0000000000" "0000000000" "0000000000" "0000000000" ...
    ##  $ SUBROUTE_NO_013B       : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ LAT_016                : num [1:14271] 45585542 46011583 44542955 44563600 46360600 ...
    ##  $ LONG_017               : chr [1:14271] "089561330" "089454321" "088544561" "088554200" ...
    ##  $ DETOUR_KILOS_019       : num [1:14271] 8 17 3 16 2 199 199 8 24 24 ...
    ##  $ TOLL_020               : num [1:14271] 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ MAINTENANCE_021        : chr [1:14271] "62" "62" "62" "62" ...
    ##  $ OWNER_022              : chr [1:14271] "62" "62" "62" "62" ...
    ##  $ FUNCTIONAL_CLASS_026   : chr [1:14271] "09" "09" "09" "09" ...
    ##  $ YEAR_BUILT_027         : num [1:14271] 1932 1974 1948 1979 1977 ...
    ##  $ TRAFFIC_LANES_ON_028A  : num [1:14271] 2 1 2 2 2 2 2 2 2 2 ...
    ##  $ TRAFFIC_LANES_UND_028B : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ ADT_029                : num [1:14271] 50 20 100 150 300 20 30 450 50 50 ...
    ##  $ YEAR_ADT_030           : num [1:14271] 2019 2019 2018 2018 2018 ...
    ##  $ DESIGN_LOAD_031        : chr [1:14271] "0" "0" "0" "4" ...
    ##  $ APPR_WIDTH_MT_032      : num [1:14271] 7.9 3.7 6.7 10.4 8.8 9.1 9.1 11.6 7.3 7.3 ...
    ##  $ MEDIAN_CODE_033        : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ DEGREES_SKEW_034       : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ STRUCTURE_FLARED_035   : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ RAILINGS_036A          : chr [1:14271] "1" "0" "0" "1" ...
    ##  $ TRANSITIONS_036B       : chr [1:14271] "0" "0" "1" "1" ...
    ##  $ APPR_RAIL_036C         : chr [1:14271] "0" "0" "1" "1" ...
    ##  $ APPR_RAIL_END_036D     : chr [1:14271] "0" "0" "1" "0" ...
    ##  $ HISTORY_037            : num [1:14271] 5 5 5 5 5 5 5 5 5 5 ...
    ##  $ NAVIGATION_038         : chr [1:14271] "0" "0" "0" "0" ...
    ##  $ NAV_VERT_CLR_MT_039    : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ NAV_HORR_CLR_MT_040    : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ OPEN_CLOSED_POSTED_041 : chr [1:14271] "B" "B" "P" "A" ...
    ##  $ SERVICE_ON_042A        : num [1:14271] 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ SERVICE_UND_042B       : num [1:14271] 5 5 5 5 5 5 5 5 5 5 ...
    ##  $ STRUCTURE_KIND_043A    : num [1:14271] 7 7 7 5 2 5 5 5 2 5 ...
    ##  $ STRUCTURE_TYPE_043B    : chr [1:14271] "01" "03" "01" "02" ...
    ##  $ APPR_KIND_044A         : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ APPR_TYPE_044B         : chr [1:14271] "00" "00" "00" "00" ...
    ##  $ MAIN_UNIT_SPANS_045    : num [1:14271] 2 2 1 2 3 2 2 1 3 3 ...
    ##  $ APPR_SPANS_046         : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ HORR_CLR_MT_047        : num [1:14271] 7.5 3.7 6.7 9.1 8.6 8.5 8.5 9.1 7.3 6.7 ...
    ##  $ MAX_SPAN_LEN_MT_048    : num [1:14271] 5.5 7.3 6.1 20.4 7.6 9.1 8.8 19.5 13.4 15.2 ...
    ##  $ STRUCTURE_LEN_MT_049   : num [1:14271] 11.3 14.6 6.1 40.5 21 18.6 18.3 19.5 32.9 21.8 ...
    ##  $ LEFT_CURB_MT_050A      : num [1:14271] 0.2 0 0 0 0 0 0 0 0 0 ...
    ##  $ RIGHT_CURB_MT_050B     : num [1:14271] 0.2 0 0 0 0 0 0 0 0 0 ...
    ##  $ ROADWAY_WIDTH_MT_051   : num [1:14271] 7.5 3.7 7 9.1 8.6 8.5 8.5 9.1 7.3 7.3 ...
    ##  $ DECK_WIDTH_MT_052      : num [1:14271] 7.9 3.7 7.8 10.3 10.5 9.1 9.1 10.4 7.9 7.9 ...
    ##  $ VERT_CLR_OVER_MT_053   : num [1:14271] 100 100 100 99.9 99.9 ...
    ##  $ VERT_CLR_UND_REF_054A  : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ VERT_CLR_UND_054B      : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ LAT_UND_REF_055A       : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ LAT_UND_MT_055B        : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ LEFT_LAT_UND_MT_056    : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ DECK_COND_058          : chr [1:14271] "4" "5" "5" "5" ...
    ##  $ SUPERSTRUCTURE_COND_059: chr [1:14271] "5" "5" "5" "7" ...
    ##  $ SUBSTRUCTURE_COND_060  : chr [1:14271] "5" "4" "7" "8" ...
    ##  $ CHANNEL_COND_061       : chr [1:14271] "4" "7" "5" "6" ...
    ##  $ CULVERT_COND_062       : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ OPR_RATING_METH_063    : num [1:14271] 2 2 2 1 1 1 1 2 1 1 ...
    ##  $ OPERATING_RATING_064   : num [1:14271] 24.7 7.3 21.6 31.5 40.6 47.7 47.7 31.2 70.2 53.9 ...
    ##  $ INV_RATING_METH_065    : num [1:14271] 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ INVENTORY_RATING_066   : num [1:14271] 17.8 5 15.1 23.1 29.7 35.8 35.8 22.9 42.4 42.5 ...
    ##  $ STRUCTURAL_EVAL_067    : chr [1:14271] "5" "2" "4" "6" ...
    ##  $ DECK_GEOMETRY_EVAL_068 : chr [1:14271] "6" "4" "5" "6" ...
    ##  $ UNDCLRENCE_EVAL_069    : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ POSTING_EVAL_070       : num [1:14271] 4 4 1 5 5 5 5 5 5 5 ...
    ##  $ WATERWAY_EVAL_071      : chr [1:14271] "4" "7" "5" "8" ...
    ##  $ APPR_ROAD_EVAL_072     : num [1:14271] 4 3 6 6 6 8 8 6 6 6 ...
    ##  $ WORK_PROPOSED_075A     : num [1:14271] 31 31 31 NA NA NA NA NA 31 NA ...
    ##  $ WORK_DONE_BY_075B      : num [1:14271] 1 1 1 NA NA NA NA NA 1 NA ...
    ##  $ IMP_LEN_MT_076         : num [1:14271] 11.5 15 11 0 0 0 0 0 40 0 ...
    ##  $ DATE_OF_INSPECT_090    : num [1:14271] 919 919 918 918 918 819 819 918 819 918 ...
    ##  $ INSPECT_FREQ_MONTHS_091: num [1:14271] 24 24 24 24 24 24 24 24 24 24 ...
    ##  $ FRACTURE_092A          : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ UNDWATER_LOOK_SEE_092B : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ SPEC_INSPECT_092C      : chr [1:14271] "N" "N" "N" "N" ...
    ##  $ FRACTURE_LAST_DATE_093A: chr [1:14271] NA NA NA NA ...
    ##  $ UNDWATER_LAST_DATE_093B: chr [1:14271] NA NA NA NA ...
    ##  $ SPEC_LAST_DATE_093C    : chr [1:14271] NA NA NA NA ...
    ##  $ BRIDGE_IMP_COST_094    : num [1:14271] 402 187 0 0 0 0 0 0 0 0 ...
    ##  $ ROADWAY_IMP_COST_095   : num [1:14271] 50 22 0 0 0 0 0 0 0 0 ...
    ##  $ TOTAL_IMP_COST_096     : num [1:14271] 452 299 460 0 0 0 0 0 53 0 ...
    ##  $ YEAR_OF_IMP_097        : num [1:14271] 2019 2019 2018 2018 2018 ...
    ##  $ OTHER_STATE_CODE_098A  : num [1:14271] NA NA NA NA NA NA NA NA NA NA ...
    ##  $ OTHER_STATE_PCNT_098B  : num [1:14271] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ OTHR_STATE_STRUC_NO_099: chr [1:14271] NA NA NA NA ...
    ##   [list output truncated]
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   STATE_CODE_001 = col_double(),
    ##   ..   STRUCTURE_NUMBER_008 = col_character(),
    ##   ..   RECORD_TYPE_005A = col_double(),
    ##   ..   ROUTE_PREFIX_005B = col_double(),
    ##   ..   SERVICE_LEVEL_005C = col_double(),
    ##   ..   ROUTE_NUMBER_005D = col_character(),
    ##   ..   DIRECTION_005E = col_double(),
    ##   ..   HIGHWAY_DISTRICT_002 = col_character(),
    ##   ..   COUNTY_CODE_003 = col_character(),
    ##   ..   PLACE_CODE_004 = col_character(),
    ##   ..   FEATURES_DESC_006A = col_character(),
    ##   ..   CRITICAL_FACILITY_006B = col_logical(),
    ##   ..   FACILITY_CARRIED_007 = col_character(),
    ##   ..   LOCATION_009 = col_character(),
    ##   ..   MIN_VERT_CLR_010 = col_double(),
    ##   ..   KILOPOINT_011 = col_double(),
    ##   ..   BASE_HWY_NETWORK_012 = col_double(),
    ##   ..   LRS_INV_ROUTE_013A = col_character(),
    ##   ..   SUBROUTE_NO_013B = col_double(),
    ##   ..   LAT_016 = col_double(),
    ##   ..   LONG_017 = col_character(),
    ##   ..   DETOUR_KILOS_019 = col_double(),
    ##   ..   TOLL_020 = col_double(),
    ##   ..   MAINTENANCE_021 = col_character(),
    ##   ..   OWNER_022 = col_character(),
    ##   ..   FUNCTIONAL_CLASS_026 = col_character(),
    ##   ..   YEAR_BUILT_027 = col_double(),
    ##   ..   TRAFFIC_LANES_ON_028A = col_double(),
    ##   ..   TRAFFIC_LANES_UND_028B = col_double(),
    ##   ..   ADT_029 = col_double(),
    ##   ..   YEAR_ADT_030 = col_double(),
    ##   ..   DESIGN_LOAD_031 = col_character(),
    ##   ..   APPR_WIDTH_MT_032 = col_double(),
    ##   ..   MEDIAN_CODE_033 = col_double(),
    ##   ..   DEGREES_SKEW_034 = col_double(),
    ##   ..   STRUCTURE_FLARED_035 = col_double(),
    ##   ..   RAILINGS_036A = col_character(),
    ##   ..   TRANSITIONS_036B = col_character(),
    ##   ..   APPR_RAIL_036C = col_character(),
    ##   ..   APPR_RAIL_END_036D = col_character(),
    ##   ..   HISTORY_037 = col_double(),
    ##   ..   NAVIGATION_038 = col_character(),
    ##   ..   NAV_VERT_CLR_MT_039 = col_double(),
    ##   ..   NAV_HORR_CLR_MT_040 = col_double(),
    ##   ..   OPEN_CLOSED_POSTED_041 = col_character(),
    ##   ..   SERVICE_ON_042A = col_double(),
    ##   ..   SERVICE_UND_042B = col_double(),
    ##   ..   STRUCTURE_KIND_043A = col_double(),
    ##   ..   STRUCTURE_TYPE_043B = col_character(),
    ##   ..   APPR_KIND_044A = col_double(),
    ##   ..   APPR_TYPE_044B = col_character(),
    ##   ..   MAIN_UNIT_SPANS_045 = col_double(),
    ##   ..   APPR_SPANS_046 = col_double(),
    ##   ..   HORR_CLR_MT_047 = col_double(),
    ##   ..   MAX_SPAN_LEN_MT_048 = col_double(),
    ##   ..   STRUCTURE_LEN_MT_049 = col_double(),
    ##   ..   LEFT_CURB_MT_050A = col_double(),
    ##   ..   RIGHT_CURB_MT_050B = col_double(),
    ##   ..   ROADWAY_WIDTH_MT_051 = col_double(),
    ##   ..   DECK_WIDTH_MT_052 = col_double(),
    ##   ..   VERT_CLR_OVER_MT_053 = col_double(),
    ##   ..   VERT_CLR_UND_REF_054A = col_character(),
    ##   ..   VERT_CLR_UND_054B = col_double(),
    ##   ..   LAT_UND_REF_055A = col_character(),
    ##   ..   LAT_UND_MT_055B = col_double(),
    ##   ..   LEFT_LAT_UND_MT_056 = col_double(),
    ##   ..   DECK_COND_058 = col_character(),
    ##   ..   SUPERSTRUCTURE_COND_059 = col_character(),
    ##   ..   SUBSTRUCTURE_COND_060 = col_character(),
    ##   ..   CHANNEL_COND_061 = col_character(),
    ##   ..   CULVERT_COND_062 = col_character(),
    ##   ..   OPR_RATING_METH_063 = col_double(),
    ##   ..   OPERATING_RATING_064 = col_double(),
    ##   ..   INV_RATING_METH_065 = col_double(),
    ##   ..   INVENTORY_RATING_066 = col_double(),
    ##   ..   STRUCTURAL_EVAL_067 = col_character(),
    ##   ..   DECK_GEOMETRY_EVAL_068 = col_character(),
    ##   ..   UNDCLRENCE_EVAL_069 = col_character(),
    ##   ..   POSTING_EVAL_070 = col_double(),
    ##   ..   WATERWAY_EVAL_071 = col_character(),
    ##   ..   APPR_ROAD_EVAL_072 = col_double(),
    ##   ..   WORK_PROPOSED_075A = col_double(),
    ##   ..   WORK_DONE_BY_075B = col_double(),
    ##   ..   IMP_LEN_MT_076 = col_double(),
    ##   ..   DATE_OF_INSPECT_090 = col_double(),
    ##   ..   INSPECT_FREQ_MONTHS_091 = col_double(),
    ##   ..   FRACTURE_092A = col_character(),
    ##   ..   UNDWATER_LOOK_SEE_092B = col_character(),
    ##   ..   SPEC_INSPECT_092C = col_character(),
    ##   ..   FRACTURE_LAST_DATE_093A = col_character(),
    ##   ..   UNDWATER_LAST_DATE_093B = col_character(),
    ##   ..   SPEC_LAST_DATE_093C = col_character(),
    ##   ..   BRIDGE_IMP_COST_094 = col_double(),
    ##   ..   ROADWAY_IMP_COST_095 = col_double(),
    ##   ..   TOTAL_IMP_COST_096 = col_double(),
    ##   ..   YEAR_OF_IMP_097 = col_double(),
    ##   ..   OTHER_STATE_CODE_098A = col_double(),
    ##   ..   OTHER_STATE_PCNT_098B = col_double(),
    ##   ..   OTHR_STATE_STRUC_NO_099 = col_character(),
    ##   ..   STRAHNET_HIGHWAY_100 = col_double(),
    ##   ..   PARALLEL_STRUCTURE_101 = col_character(),
    ##   ..   TRAFFIC_DIRECTION_102 = col_double(),
    ##   ..   TEMP_STRUCTURE_103 = col_logical(),
    ##   ..   HIGHWAY_SYSTEM_104 = col_double(),
    ##   ..   FEDERAL_LANDS_105 = col_double(),
    ##   ..   YEAR_RECONSTRUCTED_106 = col_double(),
    ##   ..   DECK_STRUCTURE_TYPE_107 = col_character(),
    ##   ..   SURFACE_TYPE_108A = col_character(),
    ##   ..   MEMBRANE_TYPE_108B = col_character(),
    ##   ..   DECK_PROTECTION_108C = col_character(),
    ##   ..   PERCENT_ADT_TRUCK_109 = col_double(),
    ##   ..   NATIONAL_NETWORK_110 = col_double(),
    ##   ..   PIER_PROTECTION_111 = col_double(),
    ##   ..   BRIDGE_LEN_IND_112 = col_character(),
    ##   ..   SCOUR_CRITICAL_113 = col_character(),
    ##   ..   FUTURE_ADT_114 = col_double(),
    ##   ..   YEAR_OF_FUTURE_ADT_115 = col_double(),
    ##   ..   MIN_NAV_CLR_MT_116 = col_double(),
    ##   ..   FED_AGENCY = col_character(),
    ##   ..   SUBMITTED_BY = col_double(),
    ##   ..   BRIDGE_CONDITION = col_character(),
    ##   ..   LOWEST_RATING = col_double(),
    ##   ..   DECK_AREA = col_double()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
head(bridges)
```

    ## # A tibble: 6 x 123
    ##   STATE_CODE_001 STRUCTURE_NUMBER_008 RECORD_TYPE_005A ROUTE_PREFIX_005B
    ##            <dbl> <chr>                           <dbl>             <dbl>
    ## 1             55 00000000000F303                     1                 6
    ## 2             55 00000000000F304                     1                 6
    ## 3             55 00000000000F310                     1                 6
    ## 4             55 00000000000F311                     1                 6
    ## 5             55 00000000000F315                     1                 6
    ## 6             55 00000000000F317                     1                 6
    ## # ... with 119 more variables: SERVICE_LEVEL_005C <dbl>,
    ## #   ROUTE_NUMBER_005D <chr>, DIRECTION_005E <dbl>, HIGHWAY_DISTRICT_002 <chr>,
    ## #   COUNTY_CODE_003 <chr>, PLACE_CODE_004 <chr>, FEATURES_DESC_006A <chr>,
    ## #   CRITICAL_FACILITY_006B <lgl>, FACILITY_CARRIED_007 <chr>,
    ## #   LOCATION_009 <chr>, MIN_VERT_CLR_010 <dbl>, KILOPOINT_011 <dbl>,
    ## #   BASE_HWY_NETWORK_012 <dbl>, LRS_INV_ROUTE_013A <chr>,
    ## #   SUBROUTE_NO_013B <dbl>, LAT_016 <dbl>, LONG_017 <chr>, ...

``` r
bridges = bridges %>% select(
  contains("year") , contains("rating"), contains("district"))
str(bridges)
```

    ## tibble [14,271 x 11] (S3: tbl_df/tbl/data.frame)
    ##  $ YEAR_BUILT_027        : num [1:14271] 1932 1974 1948 1979 1977 ...
    ##  $ YEAR_ADT_030          : num [1:14271] 2019 2019 2018 2018 2018 ...
    ##  $ YEAR_OF_IMP_097       : num [1:14271] 2019 2019 2018 2018 2018 ...
    ##  $ YEAR_RECONSTRUCTED_106: num [1:14271] 1958 1994 1990 0 0 ...
    ##  $ YEAR_OF_FUTURE_ADT_115: num [1:14271] 2039 2039 2038 2038 2038 ...
    ##  $ OPR_RATING_METH_063   : num [1:14271] 2 2 2 1 1 1 1 2 1 1 ...
    ##  $ OPERATING_RATING_064  : num [1:14271] 24.7 7.3 21.6 31.5 40.6 47.7 47.7 31.2 70.2 53.9 ...
    ##  $ INV_RATING_METH_065   : num [1:14271] 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ INVENTORY_RATING_066  : num [1:14271] 17.8 5 15.1 23.1 29.7 35.8 35.8 22.9 42.4 42.5 ...
    ##  $ LOWEST_RATING         : num [1:14271] 4 4 5 5 5 7 6 5 5 7 ...
    ##  $ HIGHWAY_DISTRICT_002  : chr [1:14271] "07" "07" "06" "03" ...

``` r
ggplot(bridges, aes(x=YEAR_BUILT_027, y=INVENTORY_RATING_066, col=HIGHWAY_DISTRICT_002)) +
  geom_jitter() +
  scale_x_continuous() +
  labs(
    title="Inventory Rating vs Year Built of Wisconsin Bridges",
    col="Highway District") +
  xlab("Year Built") +
  ylab("Inventory Rating")
```

    ## Warning: Removed 14 rows containing missing values (geom_point).

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->
