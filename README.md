# utl_classic_editor_part_II
SAS  icon, autoexec and mouse mappings

    ```  /* T007870 Fast point and shoot programming(PART II the Fast Part)  ```
    ```    ```
    ```    ```
    ```  %let pgm=utl_perpac;  ```
    ```    ```
    ```  A Performance package  ```
    ```    ```
    ```  *  ```
    ```   _ __   ___ _ __ _ __   __ _  ___  ```
    ```  | '_ \ / _ \ '__| '_ \ / _` |/ __|  ```
    ```  | |_) |  __/ |  | |_) | (_| | (__  ```
    ```  | .__/ \___|_|  | .__/ \__,_|\___|  ```
    ```  |_|             |_|  ```
    ```  ;  ```
    ```    ```
    ```  Fast point and shoot programming(PART II the Fast Part)  ```
    ```  Works best classic editor, parts will work in EE, none  ```
    ```  of it will work in EG.  ```
    ```  This message is in  ```
    ```    ```
    ```    utl_perpac2ndmsg.txt  ```
    ```    https://drive.google.com/file/d/0ByX2ii2B0Rq9ZWlBV1B3Q1J6VFU/view?usp=sharing  ```
    ```    http://tinyurl.com/oyp5xyu  ```
    ```    ```
    ```    ```
    ```    associated files are in  ```
    ```    https://drive.google.com/file/d/0ByX2ii2B0Rq9dENzU1ZOeFEtYjg/view?usp=sharing  ```
    ```    http://tinyurl.com/nvcoz73  ```
    ```    ```
    ```    pep.zip  (does not hev the lates set of utilities see PARTI.  ```
    ```    ```
    ```    files in pep.zip archive (64 bit Win Pro/Full SAS 9.4M2 64bit)  ```
    ```    ```
    ```       utl_perpac.sas    - command macros  ```
    ```       autoexec.sas      - my autoexec  ```
    ```       config.cfg        - config  ```
    ```       profile.sas7bcat  - profile  ```
    ```       utl_perpackey.txt - function keys  ```
    ```       utl_PerPacLft.jpg - left doc  ```
    ```       utl_PerPacRgt.jpg - right doc  ```
    ```       utl_PerPacInv.txt - SAS invocation  ```
    ```       profile.cpt       - for 32bit  ```
    ```       cutouts.txt       - keyboard cutouts  ```
    ```    ```
    ```    ```
    ```    I think I have optimized SAS for an enviroment dominated by sequential  ```
    ```    reads of data partitioned SAS datasets with SPDE and parallelism.  ```
    ```    Not so good for frequent small random writes.  ```
    ```    ```
    ```    Basically if you rename your profile.sas7bdat and copy mine you will  ```
    ```    get most of my setup.  ```
    ```    ```
    ```      * my invocation  ```
    ```      c:\sashome\SASFoundation\9.4\sas.exe  ```
    ```      -work c:\wrk  ```
    ```      -sasuser c:\etc  ```
    ```      -RLANG  ```
    ```      -autoexec c:\oto\autoexec.sas  ```
    ```      -sasinitialfolder  .  ```
    ```      -nosplash  ```
    ```      -autosaveloc c:\ver\pgm.sas  ```
    ```      -config c:\cfg\config.cfg  ```
    ```      -nodmsexp  ```
    ```      -sasautos c:\oto  ```
    ```      -awscontrol notitle  ```
    ```      -emailsys SMTP  ```
    ```      -nodmsexp  ```
    ```      -awscontrol notitle  ```
    ```    ```
    ```    ```
    ```  *            _  ```
    ```    __ _ _   _| |_ ___   _____  _____  ___  ```
    ```   / _` | | | | __/ _ \ / _ \ \/ / _ \/ __|  ```
    ```  | (_| | |_| | || (_) |  __/>  <  __/ (__  ```
    ```   \__,_|\__,_|\__\___/ \___/_/\_\___|\___|  ```
    ```    ```
    ```  ;  ```
    ```    ```
    ```  /* this autoexec is located in &_r/oto/Tut_Oto.sas */  ```
    ```    ```
    ```  * generally I do not like to set nofmterr but client has many datasets with missing user formats;  ```
    ```    ```
    ```  options ls=171 ps=65 cmdmac nofmterr nocenter nodate nonumber noquotelenmax validvarname=upcase  ```
    ```  compress=no FORMCHAR='|----|+|---+=|-/\<>*';  ```
    ```    ```
    ```  /*--------------------------------------------------------------*\  ```
    ```  |                                                                |  ```
    ```  | Versioning _q provides starting suffix                         |  ```
    ```  |                                                                |  ```
    ```  \*--------------------------------------------------------------*/  ```
    ```    ```
    ```  /* number of seconds into the day for versioning */  ```
    ```  %Let _q=%sysfunc(int(%sysfunc(time())));  ```
    ```    ```
    ```  * change root for other systems;  ```
    ```  %let _r=&_r;   * root;  ```
    ```  %let _p=&_r/utl; * program directory;  ```
    ```  %let _o=&_r/oto; * user autocall folder;  ```
    ```    ```
    ```  %let letters=%str(  ```
    ```  "A" ,"B" ,"C" ,"D" ,"E" ,"F" ,"G" ,"H" ,"I" ,"J" ,"K" ,"L"  ```
    ```  ,"M" ,"N" ,"O" ,"P" ,"Q" ,"R" ,"S" ,"T" ,"U" ,"V" ,"W" ,"X"  ```
    ```  ,"Y" ,"Z");  ```
    ```    ```
    ```  %let numbers=%str(1 ,2 ,3 ,4 ,5 ,6 ,7 ,8 ,9, 10);  ```
    ```    ```
    ```  %let months="JAN" ,"FEB" ,"MAR" ,"APR" ,"MAY" ,"JUN" ,"JUL" ,"AUG","SEP" ,"OCT" ,"NOV" ,"DEC";  ```
    ```    ```
    ```    ```
    ```  ods results off;  ```
    ```    ```
    ```  * set up reversible weak encryption;  ```
    ```    ```
    ```  %let cmplib = %sysfunc(getoption(cmplib));  ```
    ```  options cmplib = (work.functions &cmplib);  ```
    ```    ```
    ```  options fmtsearch=(work.formats mta.mta_formats_v1f mta.var2des);  ```
    ```    ```
    ```  proc fcmp outlib=work.functions.hashssn;  ```
    ```  function encrypt(ssn);  ```
    ```      length rev $17;  ```
    ```      key=8192;  ```
    ```      ssn_remainder = mod(ssn, key);  ```
    ```      ssn_int       = round((ssn - ssn_remainder)/key,1);  ```
    ```      * 8192  ssn_remainder = 1 and ssn_int = 1 ie 1*key + 1 = original value;  ```
    ```      ssn_big   = ssn_int*100000 + ssn_remainder;  ```
    ```      rev=reverse(put(ssn_big,17.));  ```
    ```      if substr(rev,1,1)=0 then rev=cats('-1',substr(rev,2));  ```
    ```      ssn_encrypt=input(rev,17.);  ```
    ```    return(ssn_encrypt);  ```
    ```  endsub;  ```
    ```  run;quit;  ```
    ```    ```
    ```  proc fcmp outlib=work.functions.hashssn;  ```
    ```  function decrypt(ssn);  ```
    ```      length rev $17;  ```
    ```      key=8192;  ```
    ```      rev=strip(reverse(put(ssn,17.)));  ```
    ```      if index(rev,'-')>0 then substr(rev,index(rev,'-')-1)='0 ';  ```
    ```      ssn_big=input(rev,17.);  ```
    ```      ssn_decrypt   = round(ssn_big/100000,1)*key + mod(ssn_big,10000);  ```
    ```    return(ssn_decrypt);  ```
    ```  endsub;  ```
    ```  ;run;quit;  ```
    ```    ```
    ```  /* encrypt decrypt (weak moderate size integer encryption) */  ```
    ```  /* sha is better  ```
    ```    ```
    ```  data encrypt;  ```
    ```    ssn=123456789;  ```
    ```    ssn_encrypt=encrypt(ssn);  ```
    ```    put ssn= ssn_encrypt=;  ```
    ```    ssn_decrypt=decrypt(ssn_encrypt);  ```
    ```    put ssn_encrypt=  ssn_decrypt=;  ```
    ```  run;quit;  ```
    ```    ```
    ```  SSN=123456789          SSN_ENCRYPT=9433007051  ```
    ```  SSN_ENCRYPT=9433007051 SSN_DECRYPT=123456789  ```
    ```  */  ```
    ```    ```
    ```  * missing populated;  ```
    ```  proc format;  ```
    ```    ```
    ```    value num2mis  ```
    ```     . = 'MIS'  ```
    ```     0 = 'ZRO'  ```
    ```     0<-high = "POS"  ```
    ```     low-<0 = 'NEG'  ```
    ```     other='POP'  ```
    ```     ;  ```
    ```     value $chr2mis  ```
    ```     'Unknown',' ','UNK','U','NA','UNKNOWN','Missing','MISSING','MISS' ='MIS'  ```
    ```     other='POP'  ```
    ```      ;  ```
    ```  run;  ```
    ```    ```
    ```  /* Tom Abernathy message on/off capability; */  ```
    ```  /* note because of sungle quotes the macro is only unquoted after macro var messages is defined */  ```
    ```    ```
    ```  data _null_;  ```
    ```    call symputx('msgput','&messages.putlog','G');  * Use &msg inside of data steps for execution messages;  ```
    ```    call symputx('msgMput','%&messages.put','G');   * Use &macmsg for compile time messages;  ```
    ```  run;quit;  ```
    ```    ```
    ```  %let messages=*;  * turn messages off ;  ```
    ```  %let messages=;   * turn messages on  ;  ```
    ```    ```
    ```  /* EXAMPLES OF TOMS CLEVER TECHINQUE AT COMPILE TIME  ```
    ```    ```
    ```  %let messages=;   * turn messages on  ;  ```
    ```    ```
    ```  &msgMput Roger You Made an Error;  ```
    ```    ```
    ```     Roger You Made an Error  ```
    ```    ```
    ```    ```
    ```  %let messages=*;   * turn messages off  ;  ```
    ```    ```
    ```  &msgMput Roger;    * does not print anything to the log ;  ```
    ```    ```
    ```    ```
    ```    ```
    ```  /* EXAMPLES OF TOMS CLEVER TECHINQUE AT DATASTEP EXECUTION TIME  ```
    ```    ```
    ```  %let messages=;    * turn messages on ;  ```
    ```    ```
    ```  data msg;  ```
    ```     array nums[10] (&numbers);  ```
    ```     do i=1 to 10;  ```
    ```        if i=5 then do;  ```
    ```            &msgput "ERROR  "  i=;  ```
    ```        end;  ```
    ```     end;  ```
    ```  run;quit;  ```
    ```    ```
    ```  ERROR  I=5  ```
    ```    ```
    ```  %let messages=*;    * turn messages off ;  ```
    ```    ```
    ```  * examples ;  ```
    ```  data msg;  ```
    ```     array nums[10] (&numbers);  ```
    ```     do i=1 to 10;  ```
    ```        if i=5 then do;  ```
    ```            &msgput "ERROR  "  i=;  ```
    ```        end;  ```
    ```     end;  ```
    ```  run;quit;  ```
    ```    ```
    ```  nothing in log  ```
    ```    ```
    ```  */  ```
    ```    ```
    ```  * hiding a password (weak encryption);  ```
    ```  data _null_;  ```
    ```   call symputx('opassp','47306C6466217368'x,'G');  ```
    ```  run;  ```
    ```    ```
    ```  * use with systask;  ```
    ```  %let _s=&_r\PROGRA~1\SASHome\SASFoundation\9.4\sas.exe -sysin nul -log nul -work &_r\wrk  ```
    ```   -rsasuser -autoexec &_r\oto\tut_Oto.sas -nosplash -sasautos &_r\oto -RLANG -config &_r\cfg\sasv9.cfg;  ```
    ```    ```
    ```  * my command macros over 50;  ```
    ```  %inc "&_o/utl_perpac.sas";  ```
    ```    ```
    ```  /* put this in your autocall library and type xit on command line when leaving SAS  ```
    ```  %macro xit/cmd  ```
    ```    des="Save last program so it can be restored next time you start SAS";  ```
    ```    home;save pgm_last r;%sysfunc(sleep(1,1));bye;  ```
    ```  %mend xit;  ```
    ```  */  ```
    ```    ```
    ```    ```
    ```  * last program worked on in previous classic editor;  ```
    ```  * will automatically be retried next time you open SAS;  ```
    ```  dm "home;pgm;home;copy pgm_last";  ```
    ```    ```
    ```    ```
    ```  *  ```
    ```   _ __ ___   ___  _   _ ___  ___  ```
    ```  | '_ ` _ \ / _ \| | | / __|/ _ \  ```
    ```  | | | | | | (_) | |_| \__ \  __/  ```
    ```  |_| |_| |_|\___/ \__,_|___/\___|  ```
    ```    ```
    ```                               _  ```
    ```   _ __ ___   __ _ _ __  _ __ (_)_ __   __ _ ___  ```
    ```  | '_ ` _ \ / _` | '_ \| '_ \| | '_ \ / _` / __|  ```
    ```  | | | | | | (_| | |_) | |_) | | | | | (_| \__ \  ```
    ```  |_| |_| |_|\__,_| .__/| .__/|_|_| |_|\__, |___/  ```
    ```                  |_|   |_|            |___/  ```
    ```  ;  ```
    ```    ```
    ```  * you may need to do this?  ```
    ```  tools>options>program editor>(make sure include blank space is checked)  ```
    ```    ```
    ```   1. Point and shoot with mouse actions(fastest)  ie push 2nd middle mouse button proc means hi-lited dataset  ```
    ```    ```
    ```  This type of 'fast' programming is only supported by the old text editor with the simple  ```
    ```  clean command line on all windows.  ```
    ```  How to map macros to the mouse and keyboard and remember actions to follow,  ```
    ```    ```
    ```  Utilities mapped to Logitech MX310 mouse  ```
    ```  The price of the mx310 has gone from $15 to $150, a good substitute(with all the functionality) is the Logitech G203($29) ```
    ```      **************************************  ```
    ```     *                                       *  ```
    ```    *                                         *  ```
    ```   *                                           *  ```
    ```   *   LMB                    RMB              *  ```
    ```   *                                           *  ```
    ```   *   FOCUS & POINTING       SUBMIT           *  ```
    ```   *   BLOCH SUBMIT          SHF RMB ls40a     *  ```
    ```   *                         CTL RMB ls40ha    *  ```
    ```   *        MMB                                *  ```
    ```   *                                           *  ```
    ```   *        MMB(F1) Verson                     *  ```
    ```   *        SHF MMB(F1) dmpa                   *  ```
    ```   *        CTL MMB(F1) dmpha                  *  ```
    ```   *        ALT RMB(F1) vuh                    *  ```
    ```   *                                           *  ```
    ```   *        MMB2                               *  ```
    ```   *                                           *  ```
    ```   *        MMB2 avgha                         *  ```
    ```   *        SHF F2 lsala                       *  ```
    ```   *        CTL F2 lsalha                      *  ```
    ```   *        ALT F2 vua                         *  ```
    ```   *                                           *  ```
    ```   *                                           *  ```
    ```   *   LEFT SIDE BUTTON     RIGHT SIDE BUTON   *  ```
    ```   *                                           *  ```
    ```   *   LSB(F11)             RSB(F12)           *  ```
    ```   *   LSB debugha          F12 magic string   *  ```
    ```   *   SHF F11 cona         SHF F12 frqva      *  ```
    ```   *   CTL F11 conha        CTL F12 cntva      *  ```
    ```   *   ALT F11 xlsha        ALT F12 unva       *  ```
    ```   *                                           *  ```
    ```    *                                          *  ```
    ```     *                                        *  ```
    ```      ***************************************;  ```
    ```    ```
    ```  Here is sample of the utilities in the package  (* most used or most critical)  ```
    ```  You can build on these macros they are just minimal SAS code.  ```
    ```    ```
    ```    avgh     proc means last dataset  ```
    ```    cnt      cnt name*sex - last dataset number unique combinations  ```
    ```    cnth     cnt name*sex - hi-lited dataset  ```
    ```    cntv     cnt hi-lited variable last dataset  ```
    ```    con      contents last dataset  ```
    ```    conh     contents hi-lited dataset  ```
    ```   *debugh   macro debug hi-lited  ```
    ```   *dmp      contents with sample data  ```
    ```   *dmph     contents with sample data hi-lited dataset  ```
    ```   *frq      freq sex*age last dataset  ```
    ```   *frqh     freq sex*age hi-lited dataset  ```
    ```    frqv     freq hilited variable last dataset  ```
    ```    iota     column of consecutive integers  ```
    ```   *ls40     40 obs last dataset  ```
    ```   *ls40h    40 obs hi-lited dataset  ```
    ```    lsal     all obs last dataset  ```
    ```    parh     does hi-lited code have matched paraentheses  ```
    ```    proch    syntax for the proc - hi-lite 'proc reg' and get syntax with example  ```
    ```   *prtw     prtw 'sex="M"' - last dataset subset printed  ```
    ```   *prtwh    prtw 'sex="M"' - hi-lited dataset subset printed  ```
    ```    sumh     statistics on hi-lited column of numbers  ```
    ```    sumv     statistics on hi-lited variable last dataset  ```
    ```    unv      proc univariate on variable in last dataset  ```
    ```    vu       viewtable last dataset  ```
    ```    vuh      viewtable hi-lited dataset  ```
    ```   *xlsh     view and edit hi-lited dataset in excel (may need a sleep w slow systems)  ```
    ```   *xplo     xplo SUBaSUM put exploded chars in past buffer  ```
    ```    ```
    ```  /*  ```
    ```  * you can use the code below to list function keys  ```
    ```    ```
    ```    proc cimport infile="c:\utl\profile.cpt" cat=work.profile;  ```
    ```    run;quit;  ```
    ```    ```
    ```    filename key catalog "sasuser.profile.dmkeys.keys";  ```
    ```     data key;  ```
    ```       infile key ;  ```
    ```       if _n_=1 then input;  ```
    ```       input key $8. len ib4. ;  ```
    ```       if len > 0 then input val $varying132. len;  ```
    ```     run;  ```
    ```     proc print width=min;  ```
    ```     run;  ```
    ```    ```
    ```  Obs    KEY        LEN    VAL  ```
    ```    ```
    ```    1    F1          71    pgm;file &pgm..sas;file c:\ver\&pgm.&_q..sas;%let _q=%eval(0&_q +1);  ```
    ```    2    F2          30    store;note;notesubmit '%avgha'  ```
    ```    3    F3           6    left 3  ```
    ```    4    F4           7    right 3  ```
    ```    5    F5          30    store;note;notesubmit '%dmpa;'  ```
    ```    6    F6          31    store;note;notesubmit '%dmpha;'  ```
    ```    7    F7          67    log;file "./&pgm..log";note zx;notesubmit "%utl_logcurchk(./&pgm);"  ```
    ```    8    F8           5    rfind  ```
    ```    9    F9           7    rchange  ```
    ```   10    F11         33    store;note;notesubmit '%debugha;'  ```
    ```   11    F12         73    ~;;;;/*'*/ *);*};*];*/;/*"*/;%mend;run;quit;%end;end;run;endcomp;%utlfix;  ```
    ```   12    SHF F1      24    note;notesubmit '%dmpa;'  ```
    ```   13    SHF F2      25    note;notesubmit '%lsala;'  ```
    ```   14    SHF F6      67    ~n ? "hil";n=*"PFil Mason";n gt:"Phil";n le:"Phim"; sql - eqt    */  ```
    ```   15    SHF F7      67    ~libname x excel ".xls";proc sql;update x;set y=2;where n="Roger"*/  ```
    ```   16    SHF F8      12    :a;copy box;  ```
    ```   17    SHF F9      12    :a:copy hdr;  ```
    ```   18    SHF F10     70    ~options minoperator;%macro t(x=a)/minoperator;%if &x in (a b c) %then  ```
    ```   19    SHF F11     24    note;notesubmit '%cona;'  ```
    ```   20    SHF F12     31    store;note;notesubmit '%frqva;'  ```
    ```   21    CTL F1      31    store;note;notesubmit '%dmpha;'  ```
    ```   22    CTL F2      32    store;note;notesubmit '%lsalha;'  ```
    ```   23    CTL F3      10    ~available  ```
    ```   24    CTL F11     31    store;note;notesubmit '%conha;'  ```
    ```   25    CTL F12     31    store;note;notesubmit '%cntva;'  ```
    ```   26    ALT F1      30    store;note;notesubmit '%vuha;'  ```
    ```   27    ALT F2      28    vt _last_ colheading=names;"  ```
    ```   28    ALT F3      64    ~proc report data=c nowd named list wrap;columns _all_;run;quit;  ```
    ```   29    ALT F11     31    store;note;notesubmit '%xlsha;'  ```
    ```   30    ALT F12     30    store;note;notesubmit '%unva;'  ```
    ```   31    CTL B        3    :tf  ```
    ```   32    CTL D       10    ~available  ```
    ```   33    CTL E       10    ~available  ```
    ```   34    CTL G        8    note g.g  ```
    ```   35    CTL H        8    note h.h  ```
    ```   36    CTL I        3    :lc  ```
    ```   37    CTL J        3    :uc  ```
    ```   38    CTL K        4    :mcu  ```
    ```   39    CTL L        4    :mcl  ```
    ```   40    CTL M       79    ~proc format;value $a;proc catalog cat=work.formats;modify a.formatc(desc=dea);  ```
    ```   41    CTL Q        9    ~aailable  ```
    ```   42    CTL R       11    wattention;  ```
    ```   43    CTL T       73    ~proc tabulate data=class;class sex age;table age,sex*(n pctn<age>)/rts=8  ```
    ```   44    CTL U       80    ~do until(last.s);set c;by s;a+ag;end;do until(last.s);set c;by s;output;end;a=0  ```
    ```   45    CTL W       10    ~available  ```
    ```   46    CTL Y       34    ~where name like "B_B" "%B%" "B%B"  ```
    ```   47    RMB         53    log;clear;out;clear;pgm;submit;home;rec;home;log;z;z;  ```
    ```   48    SHF RMB     25    note;notesubmit '%ls40a;'  ```
    ```   49    CTL RMB     32    store;note;notesubmit '%ls40ha;'  ```
    ```   50    MMB         13    ~mapped to F1  ```
    ```   51    SHF MMB     17    ~mapped to shf F1  ```
    ```   52    CTL MMB     17    ~mapped to ctl F1  ```
    ```  */  ```
    ```    ```
    ```  Note '?' on the command line retrieves previous commands.  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```    ```
    ```  *   *   ***   *   *   ***   *****  ```
    ```  ** **  *   *  *   *  *   *  *  ```
    ```  * * *  *   *  *   *   *     *  ```
    ```  *   *  *   *  *   *    *    ****  ```
    ```  *   *  *   *  *   *     *   *  ```
    ```  *   *  *   *  *   *  *   *  *  ```
    ```  *   *   ***    ***    ***   *****;  ```
    ```    ```
    ```  * Right mouse button;  ```
    ```    ```
    ```  ****   *   *  ****  ```
    ```  *   *  ** **   *  *  ```
    ```  *   *  * * *   *  *  ```
    ```  ****   *   *   ***  ```
    ```  * *    *   *   *  *  ```
    ```  *  *   *   *   *  *  ```
    ```  *   *  *   *  ****;  ```
    ```    ```
    ```  data class ;  ```
    ```    set sashelp.class;  ```
    ```    weight2 = weight * 2;  ```
    ```  run;quit;  ```
    ```    ```
    ```  RMB - Hold left mouse button down to hi-lite then hit Right Mouse button  ```
    ```        Or hold alt key down and drag to hi-lite block of text then hit RMB  ```
    ```    ```
    ```  SHF RBM  (40obs in output)  ```
    ```    ```
    ```  Hi-lite sashelp.class then 'CTL RMB' (40 obs hi-lited)  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  * Middle mouse button;  ```
    ```    ```
    ```  *   *  *   *  ****  ```
    ```  ** **  ** **   *  *  ```
    ```  * * *  * * *   *  *  ```
    ```  *   *  *   *   ***  ```
    ```  *   *  *   *   *  *  ```
    ```  *   *  *   *   *  *  ```
    ```  *   *  *   *  ****  ```
    ```    ```
    ```  Push MMB and a timestamped version of your program will be save in c:\ver  ```
    ```  and a production version in c:\utl  ```
    ```  This requires %let pgm=mypgm.sas; exist and %let _q be set to the time in autoexec.  ```
    ```  c:\ver and c:\utl need to exist,  ```
    ```    ```
    ```  data class ;  ```
    ```    set sashelp.class;  ```
    ```    weight2 = weight * 2;  ```
    ```  run;quit;  ```
    ```    ```
    ```  SHF MMB  ```
    ```    ```
    ```  Middle Observation(9 ) of Last dataset = WORK.CLASS - Total Obs 19  ```
    ```    ```
    ```   -- CHARACTER --  ```
    ```  NAME                             C    8       Jeffrey             NAME  ```
    ```  SEX                              C    1       M                   SEX  ```
    ```    ```
    ```   -- NUMERIC --  ```
    ```  AGE                              N    8       13                  AGE  ```
    ```  HEIGHT                           N    8       62.5                HEIGHT  ```
    ```  WEIGHT                           N    8       84                  WEIGHT  ```
    ```  WEIGHT2                          N    8       168                 WEIGHT2  ```
    ```    ```
    ```    ```
    ```  CTL MMB same as above but hi-lited dataset  ```
    ```  ALT MMB viewtable hi-lited dataset  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  * 2nd Middle mouse button;  ```
    ```    ```
    ```  *   *  *   *  ****    ***  ```
    ```  ** **  ** **   *  *  *   *  ```
    ```  * * *  * * *   *  *      *  ```
    ```  *   *  *   *   ***     **  ```
    ```  *   *  *   *   *  *   *  ```
    ```  *   *  *   *   *  *  *  ```
    ```  *   *  *   *  ****   *****;  ```
    ```    ```
    ```  data class ;  ```
    ```    set sashelp.class;  ```
    ```    weight2 = weight * 2;  ```
    ```  run;quit;  ```
    ```    ```
    ```  MMB2 (means of last dataset)  ```
    ```    ```
    ```  The MEANS Procedure  ```
    ```    ```
    ```                                                                           Lower  ```
    ```  Variable     N             Sum            Mean         Minimum        Quartile          Median   ...  ```
    ```  ------------------------------------------------------------------------------------------------  ```
    ```  AGE         19     253.0000000      13.3157895      11.0000000      12.0000000      13.0000000  ```
    ```  HEIGHT      19         1184.40      62.3368421      51.3000000      57.5000000      62.8000000  ```
    ```  WEIGHT      19         1900.50     100.0263158      50.5000000      84.0000000      99.5000000  ```
    ```  WEIGHT2     19         3801.00     200.0526316     101.0000000     168.0000000     199.0000000  ```
    ```  ------------------------------------------------------------------------------------------------  ```
    ```    ```
    ```  SHF MMB2 listing of all obs last dataset  ```
    ```  CTL MMB2 listing of all obs hi-lited dataset  ```
    ```  ALT MMB2 viewtable last dataset  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  * left side button;  ```
    ```    ```
    ```  *       ***   ****  ```
    ```  *      *   *   *  *  ```
    ```  *       *      *  *  ```
    ```  *        *     ***  ```
    ```  *         *    *  *  ```
    ```  *      *   *   *  *  ```
    ```  *****   ***   ****;  ```
    ```    ```
    ```  %macro errmke(dummy);  ```
    ```      data class;  ```
    ```         set sashelp.class(obs=1);  ```
    ```         if name=2 then sex='M';  ```
    ```      run;quit;  ```
    ```  %mend errmke;  ```
    ```    ```
    ```  %errmke;  ```
    ```    ```
    ```    ```
    ```  Hi-lite code and push left side button  ```
    ```    ```
    ```  This identifies the SAS statement with the error.  ```
    ```    ```
    ```  1401 +data class;  ```
    ```  1402 +set sashelp.class(obs=1);  ```
    ```  1403 +if name=2 then sex='M';  ```
    ```  ERROR: Character value found where numeric value needed at line 1403 column 4.  ```
    ```  1404 +run;  ```
    ```    ```
    ```  data class ;  ```
    ```    set sashelp.class;  ```
    ```    weight2 = weight * 2;  ```
    ```  run;quit;  ```
    ```    ```
    ```  SHF LSB contents last dataset;  ```
    ```  CTL LSB contents hi-lited dataset;  ```
    ```  ALT LSB hi-lited dataset into excel  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  * right side button;  ```
    ```    ```
    ```  ****    ***   ****  ```
    ```  *   *  *   *   *  *  ```
    ```  *   *   *      *  *  ```
    ```  ****     *     ***  ```
    ```  * *       *    *  *  ```
    ```  *  *   *   *   *  *  ```
    ```  *   *   ***   ****  ```
    ```    ```
    ```  data class ;  ```
    ```    set sashelp.class;  ```
    ```    weight2 = weight * 2;  ```
    ```  run;quit;  ```
    ```    ```
    ```  RSB Magic string also just hit F12  ```
    ```  SHR RSB  frequency hi-lited variable in last dataset  ```
    ```  CTL RSB  distinct levels hi-lited variable in last dataset  ```
    ```  ALT RSB  univariate hi-lited variable in last dataset  ```
    ```    ```
    ```  ***************************************************************************  ```
    ```  ***************************************************************************;  ```
    ```    ```
    ```  Example 1.  Which line in the macro is causing the error.  ```
    ```    ```
    ```   In the macro below variable 'name' is a character but a numeric variaqble is needed.  ```
    ```   However SAS reports the error on the invocation line '%errmke'. We want SAS  ```
    ```   to tell us which line inside the macro is causing the problem.  ```
    ```    ```
    ```    ```
    ```   %macro errmke(dummy);  ```
    ```       data class;  ```
    ```          set sashelp.class(obs=1);  ```
    ```          if name=2 then sex='M';  ```
    ```       run;quit;  ```
    ```    %mend errmke;  ```
    ```    ```
    ```    %errmke;  ```
    ```    ```
    ```   If you highlight the macro with invocation and type debugh you will see the following  ```
    ```   in the log. Note SAS has identifies line 1403 columg 4 (position of name varable)  ```
    ```   as the issue.  ```
    ```    ```
    ```    ```
    ```   1401 +data class;  ```
    ```   1402 +set sashelp.class(obs=1);  ```
    ```   1403 +if name=2 then sex='M';  ```
    ```   ERROR: Character value found where numeric value needed at line 1403 column 4.  ```
    ```   1404 +run;  ```
    ```    ```
    ```  *****************************************************************************;  ```
    ```    ```
    ```  Example 2. I would like to view and edit the dataset in excel  ```
    ```    ```
    ```    data class;  ```
    ```       set sashelp.class;  ```
    ```    run;quit;  ```
    ```    ```
    ```    Highlight class and type xlsh on the command line  ```
    ```    ```
    ```    ```
    ```  ******************************************************************************;  ```
    ```    ```
    ```  Example 3 I would like the first 20 integers in my editor.  ```
    ```    ```
    ```  Just type 'ioata 10' on the command line  ```
    ```    ```
    ```  01  ```
    ```  02  ```
    ```  03  ```
    ```  04  ```
    ```  05  ```
    ```  06  ```
    ```  07  ```
    ```  08  ```
    ```  09  ```
    ```  10  ```
    ```    ```
    ```  ******************************************************************************;  ```
    ```    ```
    ```  * I would like the statistics on the two numbers above.  ```
    ```    ```
    ```    Just highlite the coulumn of numbers and type sumh on command line  ```
    ```    ```
    ```                                                Analysis Variable : X  ```
    ```    ```
    ```                                                 Lower                       Upper  ```
    ```   N          Mean          Sum      Minimum     Quartile       Median        Quartile         Maximum  ```
    ```  ----------------------------------------------------------------------------------------------------  ```
    ```  10     5.5000000   55.0000000    1.0000000    3.0000000    5.5000000       8.0000000      10.0000000  ```
    ```  ----------------------------------------------------------------------------------------------------  ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  Example 4.  ```
    ```    ```
    ```    I would like a vertical dump on the middle observation with type, length and labels  ```
    ```    ```
    ```    Highlight  ```
    ```    ```
    ```         sashelp.zipcode  ```
    ```    and  ```
    ```         type dmph on the command line  ```
    ```    ```
    ```         type dmp for last dataset  ```
    ```    ```
    ```    ```
    ```  Middle Observation(20633 ) of sashelp.zipcode - Total Obs 41,267  ```
    ```    ```
    ```    ```
    ```   -- CHARACTER --  ```
    ```  ZIP_CLASS             C    1       ZIP Code Classifi  ```
    ```  CITY                  C    35      Ionia               Name of city/org  ```
    ```  STATECODE             C    2       MI                  Two-letter abbrev. for state name.  ```
    ```  STATENAME             C    25      Michigan            Full name of state/territory  ```
    ```  COUNTYNM              C    25      Ionia               Name of county/parish.  ```
    ```  AREACODES             C    12      616                 Multiple Area Codes for ZIP Code.  ```
    ```  TIMEZONE              C    9       Eastern             Time Zone for ZIP Code.  ```
    ```  DST                   C    1       Y                   ZIP Code obeys Daylight Savings: Y-Yes N-No  ```
    ```  PONAME                C    35      Ionia               USPS Post Office Name: same as City  ```
    ```  ALIAS_CITY            C    300                         USPS - alternate names of city separated by ||  ```
    ```  ALIAS_CITYN           C    300                         Local - alternate names of city separated by ||  ```
    ```  CITY2                 C    35      IONIA               Clean CITY name for geocoding  ```
    ```  STATENAME2            C    25      MICHIGAN            Clean STATENAME for geocoding  ```
    ```    ```
    ```   -- NUMERIC --  ```
    ```  ZIP                   N    8       48846               The 5-digit ZIP Code  ```
    ```  Y                     N    8       42.985392           Latitude (degrees) of the center (centroid) of ZIP Code.  ```
    ```  X                     N    8       -85.064142          Longitude (degrees) of the center (centroid) of ZIP Code.  ```
    ```  STATE                 N    8       26                  Two-digit number (FIPS code) for state/territory  ```
    ```  COUNTY                N    8       67                  FIPS county code.  ```
    ```  AREACODE              N    8       616                 Single Area Code for ZIP Code.  ```
    ```  GMTOFFSET             N    8       -5                  Diff (hrs) between GMT and time zone for ZIP Code  ```
    ```    ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  Example 5  ```
    ```    ```
    ```  Do my parenthesis match?  ```
    ```    ```
    ```      data class;  ```
    ```        set sashelp.class(where=(sex='M' and name in ('John','Jane')) ;  ```
    ```      run;quit;  ```
    ```    ```
    ```      highlight first and last parens abd type parh on the command line  ```
    ```    ```
    ```      **********************  ```
    ```    ```
    ```      Missing 1 ) parentheses  ```
    ```    ```
    ```      **********************  ```
    ```    ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  last dataset    hilited dataset  ```
    ```    ```
    ```  frq sex*name    frqh sex*name     PROC FREQ  ```
    ```  frq sex         frqh sex  ```
    ```    ```
    ```  cnt sex         cnth sex          UNIQUE LEVELS  ```
    ```  cnt sex*name    cnth sex*name  ```
    ```    ```
    ```  prtw 'sex="M"'  prtwh 'sex="M"'   PRINT SUBSET  ```
    ```    ```
    ```    ```
    ```  Hilite and type frqh type*origin on command line  ```
    ```    ```
    ```             sashelp.cars  ```
    ```    ```
    ```    ```
    ```  Number of Variable Levels  ```
    ```    ```
    ```  Variable      Levels  ```
    ```  --------------------  ```
    ```  TYPE               6  ```
    ```  ORIGIN             3  ```
    ```    ```
    ```    ```
    ```                                               Cumulative    Cumulative  ```
    ```  TYPE      ORIGIN    Frequency     Percent     Frequency      Percent  ```
    ```  ---------------------------------------------------------------------  ```
    ```  Hybrid    Asia             3        0.70             3         0.70  ```
    ```  SUV       Asia            25        5.84            28         6.54  ```
    ```  SUV       Europe          10        2.34            38         8.88  ```
    ```  SUV       USA             25        5.84            63        14.72  ```
    ```  Sedan     Asia            94       21.96           157        36.68  ```
    ```  Sedan     Europe          78       18.22           235        54.91  ```
    ```  Sedan     USA             90       21.03           325        75.93  ```
    ```  Sports    Asia            17        3.97           342        79.91  ```
    ```  Sports    Europe          23        5.37           365        85.28  ```
    ```  Sports    USA              9        2.10           374        87.38  ```
    ```  Truck     Asia             8        1.87           382        89.25  ```
    ```  Truck     USA             16        3.74           398        92.99  ```
    ```  Wagon     Asia            11        2.57           409        95.56  ```
    ```  Wagon     Europe          12        2.80           421        98.36  ```
    ```  Wagon     USA              7        1.64           428       100.00  ```
    ```    ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  Example 6  ```
    ```    ```
    ```   The commands with the h suffix work on highlited datasets(in pgm/log/output)  ```
    ```    ```
    ```   con  ```
    ```   conh  ```
    ```   ls40  ```
    ```   ls40h  ```
    ```   lsal  ```
    ```   lsalh  ```
    ```    ```
    ```      Highlite  ```
    ```    ```
    ```           sashelp.cars  ```
    ```    ```
    ```      type ls40h  list first 40 obs  ```
    ```           conh   contents  ```
    ```           lsalh  list all obs  ```
    ```    ```
    ```    ```
    ```  **********************************************************************************  ```
    ```    ```
    ```  xplo MAINaSORT  ```
    ```    ```
    ```  puts the following in the paste buffer  ```
    ```    ```
    ```  *   *    *    *****  *   *          ***    ***   ****   *****  ```
    ```  ** **   * *     *    **  *         *   *  *   *  *   *    *  ```
    ```  * * *  *   *    *    * * *          *     *   *  *   *    *  ```
    ```  *   *  *****    *    *  **           *    *   *  ****     *  ```
    ```  *   *  *   *    *    *   *            *   *   *  * *      *  ```
    ```  *   *  *   *    *    *   *         *   *  *   *  *  *     *  ```
    ```  *   *  *   *  *****  *   *          ***    ***   *   *    *  ```
    ```    ```
    ```      **************************************  ```
    ```     *                                       *  ```
    ```    *                                         *  ```
    ```   *                                           *  ```
    ```   *   LMB                    RMB              *  ```
    ```   *                                           *  ```
    ```   *   FOCUS & POINTING       SUBMIT           *  ```
    ```   *   BLOCH SUBMIT          SHF RMB ls40a     *  ```
    ```   *                         CTL RMB ls40ha    *  ```
    ```   *        MMB                                *  ```
    ```   *                                           *  ```
    ```   *        MMB(F1) Verson                     *  ```
    ```   *        SHF MMB(F1) dmpa                   *  ```
    ```   *        CTL MMB(F1) dmpha                  *  ```
    ```   *        ALT RMB(F1) vuh                    *  ```
    ```   *                                           *  ```
    ```   *        MMB2                               *  ```
    ```   *                                           *  ```
    ```   *        MMB2 avgha                         *  ```
    ```   *        SHF F2 lsala                       *  ```
    ```   *        CTL F2 lsalha                      *  ```
    ```   *        ALT F2 vua                         *  ```
    ```   *                                           *  ```
    ```   *                                           *  ```
    ```   *   LEFT SIDE BUTTON     RIGHT SIDE BUTON   *  ```
    ```   *                                           *  ```
    ```   *   LSB(F11)             RSB(F12)           *  ```
    ```   *   LSB debugha          F12 magic string   *  ```
    ```   *   SHF F11 cona         SHF F12 frqva      *  ```
    ```   *   CTL F11 conha        CTL F12 cntva      *  ```
    ```   *   ALT F11 xlsha        ALT F12 unva       *  ```
    ```   *                                           *  ```
    ```    *                                          *  ```
    ```     *                                        *  ```
    ```      ***************************************;  ```
    ```    ```
    ```  ========================================================  ```
    ```    ```
    ```  last dataset    hi-lited dataset  ```
    ```    ```
    ```  FREQ  ```
    ```  frq sex*name    frqh sex*name  ```
    ```  frq sex         frqh sex  ```
    ```    ```
    ```  UNIQUE LEVELS  ```
    ```  cnt sex cnth    sex  ```
    ```  cnt sex*name    cnth sex*name  ```
    ```    ```
    ```  prtw 'sex="M"'   prtwh 'sex="M"'  ```
    ```    ```
    ```  =========================================================  ```
    ```    ```
    ```    ```
    ```     RMB              MMB-F1    MMB2-F2  LSB-F11  RSB-F12  ```
    ```    ```
    ```      SUBMIT           VERSION   avgh     debug    magic  ```
    ```      S ls40           S dmp     S lsal   S con    S frqv  ```
    ```      C ls40h          C dmph    C lsalh  C conh   C cntv  ```
    ```                       A vuh     A vu     A xlsh   A unv  ```
    ```    ```
    ```      RMB               F1        F2       F3      F4  ```
    ```    ```
    ```  ==========================================================  ```
    ```    ```
    ```     F5        F6       F7      F8  ```
    ```    ```
    ```     dmp      dmph    logchk    rfind  ```
    ```  ==========================================================  ```
    ```    ```
    ```     F9        F10      F11     F12  ```
    ```    ```
    ```     rchange          debugh    MAGIC  ```
    ```    ```
    ```  ==========================================================  ```
