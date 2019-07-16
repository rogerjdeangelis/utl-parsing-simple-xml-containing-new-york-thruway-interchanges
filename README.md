# utl-parsing-simple-xml-containing-new-york-thruway-interchanges
Parsing simple xml containing new york thruway interchanges

    Parsing simple xml containing new york thruway interchanges

    Although this is a very simple example xml2 and rvest can handle very complex web scraping.

    github
    https://tinyurl.com/y4krgqo4
    https://github.com/rogerjdeangelis/utl-parsing-simple-xml-containing-new-york-thruway-interchanges

    StackOverflow
    https://stackoverflow.com/questions/57015097/r-to-parse-xml-page

    Dave2e
    https://stackoverflow.com/users/5792244/dave2e

    library(xml2);
    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    * pasted from web;

    <interchanges>
    <interchange id="m00x" latitude="40.90564" longitude="-73.87817" routeid="ML" milepost="0.00" type="Line"
    exitid="" description="New York City Line - Major Deegan Expressway (I-87)" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m01x" latitude="40.91210" longitude="-73.87535" routeid="ML" milepost="0.48" type="Interchange"
    exitid="1" description="Hall Place - McLean Avenue" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m02x" latitude="40.92149" longitude="-73.86309" routeid="ML" milepost="0.92" type="Interchange"
    exitid="2" description="Yonkers Avenue - Raceway (No Southbound Exit)" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m03x" latitude="40.92510" longitude="-73.85850" routeid="ML" milepost="1.77" type="Interchange"
    exitid="3" description="Mile Square Road (No Southbound Exit)" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m04x" latitude="40.93086" longitude="-73.85683" routeid="ML" milepost="2.18" type="Interchange"
    exitid="4" description="Cross County Parkway - Mile Square Road" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m05x" latitude="40.93833" longitude="-73.85564" routeid="ML" milepost="2.70" type="Interchange"
    exitid="5" description="White Plains - Central Park Avenue (NY Route 100)(No Southbound Exit)" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m06x" latitude="40.95496" longitude="-73.86093" routeid="ML" milepost="4.00" type="Interchange"
    exitid="6" description="(6 Northbound; 6E & 6W Southbound) Yonkers - Bronxville - Tuckahoe Road" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m06a" latitude="40.96670" longitude="-73.86080" routeid="ML" milepost="5.14" type="Interchange"
    exitid="6A" description="Stew Leonard Drive" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="TB-YNK" latitude="40.97557" longitude="-73.85861" routeid="ML" milepost="5.47" type="Toll Barrier"
    exitid="TB-YNK" description="Yonkers Cashless Toll" route="I-87 - NYS Thruway" tolled="true" tolleddirection="both"/>
    <interchange id="m07x" latitude="41.00872" longitude="-73.85099" routeid="ML" milepost="7.58" type="Interchange"
    exitid="7" description="Ardsley - NY Route 9A (No Southbound Exit)" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m07a" latitude="41.04259" longitude="-73.83608" routeid="ML" milepost="10.33" type="Interchange"
    exitid="7A" description="Saw Mill River Parkway - Taconic State Parkway" route="I-87 - NYS Thruway" tolled="false"/>
    <interchange id="m08x" latitude="41.05656" longitude="-73.83533" routeid="ML" milepost="11.31" type="Interchange"
    exitid="8" description="White Plains - Rye - Cross Westchester Expressway (I-287)" route="I-87 - NYS Thruway" tolled="false"/>
    </interchanges>
    ;;;;
    run;quit;

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;
    \WORK.WANT total obs=151

     ID     LATITUDE LONGITUD  ROUTEID MILEPOST TYPE         EXITID DESCRIPT                                  ROUTE                TOLLED

     m01x   40.91210 -73.87535   ML     0.48    Interchange  1      Hall Place - McLean Avenue                I-87 - NYS Thruway   false
     m03x   40.92510 -73.85850   ML     1.77    Interchange  3      Mile Square Road (No Southbound Exit)     I-87 - NYS Thruway   false
     m04x   40.93086 -73.85683   ML     2.18    Interchange  4      Cross County Parkway - Mile Square Road   I-87 - NYS Thruway   false
     m06a   40.96670 -73.86080   ML     5.14    Interchange  6A     Stew Leonard Drive                        I-87 - NYS Thruway   false
     TB-YNK 40.97557 -73.85861   ML     5.47    Toll Barrier TB-YNK Yonkers Cashless Toll                     I-87 - NYS Thruway   false

     .....

     *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utlfkil(d:/xpt/want.xpt);* just in case it exists and R fails;

    %utl_submit_r64('
    library(rvest);
    library(SASxport);
    doc<-read_xml("http://www.thruway.ny.gov/xml/interchanges.xml");
    nodes<- xml_nodes (doc, "interchange");
    want<-data.frame(do.call(rbind, xml_attrs(nodes)));
    want[] <- lapply(want, function(x) if(is.factor(x)) as.character(x) else x);
    write.xport(want,file="d:/xpt/want.xpt");
    ');


    libname xpt xport "d:/xpt/want.xpt";
    data want;
      set xpt.want;
    run;quit;
    libname xpt clear;

