# utl_proc_traj_example_trajectory_of_food_and_leisure_costs
Proc Traj example Trajectory of Food and Leisure Costs. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Proc Traj example Trajectory of Food and Leisure Costs
    *******************************************************************************************************************;
    *                                                                                                                 *;
    *  PROJECT TOKEN = taj                                                                                            *;
    *                                                                                                                 *;
    *  MAP (line numbers)                                                                                             *;
    *                                                                                                                 *;
    *     83 Macros                                                                                                   *;
    *    400 Begin analysis (normalize input)                                                                         *;
    *    461 Check Data (validation and verification macro)                                                           *;
    *   1093 Slides with analysis                                                                                     *;
    *                                                                                                                 *;
    *  Windows Local workstation SAS 9.4M2(64bit) Win 7(64bit) Dell T7400 64gb ram, dual SSD raid 0 arrays, 8 core    *;
    *                                                                                                                 *;
    *; %let purpose=SAS Proc Traj Trajectory of Food and Leisure Costs;                                               *;
    *                                                                                                                 *;
    *; %let pgm=taj_100pay;     * program name                                                                        *;
    *                                                                                                                 *;
    *; %let pgmloc = c:/utl;    * program location;                                                                   *;
    *; %let pgmver = d:/ver;    * program versioning;                                                                 *;
    *; libname taj "d:/taj";    * data input and output location                                                      *;
    *                                                                                                                 *;
    *  INPUTS                                                                                                         *;
    *  =======                                                                                                        *;
    *                                                                                                                 *;
    *; %let inp001=d:/taj/taj_simulate;   * then only data input;                                                     *;
    *                                                                                                                 *;
    *; %let z=%str(                    );       * used with slides;                                                   *;
    *; %let b=%str(font_weight=bold);                                                                                 *;
    *; %let c=%str(font_face="Courier New");                                                                          *;
    *; %let f=%str(font_face="Arial");                                                                                *;
    *; %let w=%str(cellwidth=100pct);                                                                                 *;
    *; %let t=^S={font_size=20pt just=l cellwidth=100pct};                                                            *;
    *; %let u=^S={font_size=16pt font_face="Courier New" just=l cellwidth=100pct font_weight=bold};                   *;
    *; %let v=^S={font_size=14pt font_face="Courier New" just=l cellwidth=100pct font_weight=bold};                   *;
    *; %let x=^S={font_size=11pt font_face="Courier New" just=l cellwidth=100pct font_weight=bold};                   *;
    *                                                                                                                 *;
    *    Use   For in slides                                                                                          *;
    *    ===   =============                                                                                          *;
    *      |   ,                                                                                                      *;
    *                                                                                                                 *;
    *      ~   ;                                                                                                      *;
    *                                                                                                                 *;
    *      #   %                                                                                                      *;
    *                                                                                                                 *;
    *      @   &                                                                                                      *;
    *                                                                                                                 *;
    *                                                                                                                 *;
    *  OVERVIEW                                                                                                       *;
    *  ========                                                                                                       *;
    *                                                                                                                 *;
    *  Internal calls  (All macros included)                                                                          *;
    *                                                                                                                 *;
    *    utl_pdflan100    template for PDF and PPT slides                                                             *;
    *    pdfbeg           start slide creation                                                                        *;
    *    pdfend           end slide preparation                                                                       *;
    *    greenbar         highlight alternate rows in ?proc report                                                    *;
    *                                                                                                                 *;
    *    not needed but useful to check incoming data                                                                 *;
    *                                                                                                                 *;
    *    voodoo           vslidation and verification of table columns and rows                                       *;
    *                                                                                                                 *;
    *  OUTPUTS                                                                                                        *;
    *  =======                                                                                                        *;
    *    Individual PDF to be                                                                                         *;
    *    You can esily combine the individiual PDFs into word or use Adobe or fre tools to combine all the pdfs.     ;*;
    *;                                                                                                               ;*;
    *                                                                                                                 *;
    *******************************************************************************************************************;

    *
     _ __ ___   __ _  ___ _ __ ___  ___
    | '_ ` _ \ / _` |/ __| '__/ _ \/ __|
    | | | | | | (_| | (__| | | (_) \__ \
    |_| |_| |_|\__,_|\___|_|  \___/|___/
    ;
    %Macro utl_pdflan100
        (
          style=utl_pdflan100
          ,frame=void
          ,TitleFont=16pt
          ,docfont=15pt
          ,fixedfont=15pt
          ,rules=none
          ,bottommargin=.25in
          ,topmargin= .25in
          ,rightmargin=.25in
          ,leftmargin=.25in
          ,cellheight=13pt
          ,cellpadding = .2pt
          ,cellspacing = .2pt
          ,borderwidth = .2pt
        ) /  Des="SAS PDF Template for PDF";

    ods path work.templat(update) sasuser.templat(update) sashelp.tmplmst(read);

    proc template ;
    source styles.printer;
    run;quit;

    Proc Template;

       define style &Style;
       parent=styles.rtf;

            class body from Document /

                   protectspecialchars=off
                   asis=on
                   bottommargin=&bottommargin
                   topmargin   =&topmargin
                   rightmargin =&rightmargin
                   leftmargin  =&leftmargin
                   ;

            class color_list /
                  'link' = blue
                   'bgH'  = _undef_
                   'fg'  = black
                   'bg'   = _undef_;

            class fonts /
                   'TitleFont2'           = ("Arial, Helvetica, Helv",&titlefont,Bold)
                   'TitleFont'            = ("Arial, Helvetica, Helv",&titlefont,Bold)

                   'HeadingFont'          = ("Arial, Helvetica, Helv",&titlefont)
                   'HeadingEmphasisFont'  = ("Arial, Helvetica, Helv",&titlefont,Italic)

                   'StrongFont'           = ("Arial, Helvetica, Helv",&titlefont,Bold)
                   'EmphasisFont'         = ("Arial, Helvetica, Helv",&titlefont,Italic)

                   'FixedFont'            = ("Courier New, Courier",&fixedfont)
                   'FixedEmphasisFont'    = ("Courier New, Courier",&fixedfont,Italic)
                   'FixedStrongFont'      = ("Courier New, Courier",&fixedfont,Bold)
                   'FixedHeadingFont'     = ("Courier New, Courier",&fixedfont,Bold)
                   'BatchFixedFont'       = ("Courier New, Courier",&fixedfont)

                   'docFont'              = ("Arial, Helvetica, Helv",&docfont)

                   'FootFont'             = ("Arial, Helvetica, Helv", 9pt)
                   'StrongFootFont'       = ("Arial, Helvetica, Helv",8pt,Bold)
                   'EmphasisFootFont'     = ("Arial, Helvetica, Helv",8pt,Italic)
                   'FixedFootFont'        = ("Courier New, Courier",8pt)
                   'FixedEmphasisFootFont'= ("Courier New, Courier",8pt,Italic)
                   'FixedStrongFootFont'  = ("Courier New, Courier",7pt,Bold);

            class GraphFonts /
                   'GraphDataFont'        = ("Arial, Helvetica, Helv",&fixedfont)
                   'GraphValueFont'       = ("Arial, Helvetica, Helv",&fixedfont)
                   'GraphLabelFont'       = ("Arial, Helvetica, Helv",&fixedfont,Bold)
                   'GraphFootnoteFont'    = ("Arial, Helvetica, Helv",8pt)
                   'GraphTitleFont'       = ("Arial, Helvetica, Helv",&titlefont,Bold)
                   'GraphAnnoFont'        = ("Arial, Helvetica, Helv",&fixedfont)
                   'GraphUnicodeFont'     = ("Arial, Helvetica, Helv",&fixedfont)
                   'GraphLabel2Font'      = ("Arial, Helvetica, Helv",&fixedfont)
                   'GraphTitle1Font'      = ("Arial, Helvetica, Helv",&fixedfont)
                   'NodeDetailFont'       = ("Arial, Helvetica, Helv",&fixedfont)
                   'NodeInputLabelFont'   = ("Arial, Helvetica, Helv",&fixedfont)
                   'NodeLabelFont'        = ("Arial, Helvetica, Helv",&fixedfont)
                   'NodeTitleFont'        = ("Arial, Helvetica, Helv",&fixedfont);


            style Graph from Output/
                    outputwidth = 100% ;

            style table from table /
                    outputwidth=100%
                    protectspecialchars=off
                    asis=on
                    background = colors('tablebg')
                    frame=&frame
                    rules=&rules
                    cellheight  = &cellheight
                    cellpadding = &cellpadding
                    cellspacing = &cellspacing
                    bordercolor = colors('tableborder')
                    borderwidth = &borderwidth;

             class Footer from HeadersAndFooters

                    / font = fonts('FootFont')  just=left asis=on protectspecialchars=off ;

                    class FooterFixed from Footer
                    / font = fonts('FixedFootFont')  just=left asis=on protectspecialchars=off;

                    class FooterEmpty from Footer
                    / font = fonts('FootFont')  just=left asis=on protectspecialchars=off;

                    class FooterEmphasis from Footer
                    / font = fonts('EmphasisFootFont')  just=left asis=on protectspecialchars=off;

                    class FooterEmphasisFixed from FooterEmphasis
                    / font = fonts('FixedEmphasisFootFont')  just=left asis=on protectspecialchars=off;

                    class FooterStrong from Footer
                    / font = fonts('StrongFootFont')  just=left asis=on protectspecialchars=off;

                    class FooterStrongFixed from FooterStrong
                    / font = fonts('FixedStrongFootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooter from Footer
                    / font = fonts('FootFont')  asis=on protectspecialchars=off just=left;

                    class RowFooterFixed from RowFooter
                    / font = fonts('FixedFootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooterEmpty from RowFooter
                    / font = fonts('FootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooterEmphasis from RowFooter
                    / font = fonts('EmphasisFootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooterEmphasisFixed from RowFooterEmphasis
                    / font = fonts('FixedEmphasisFootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooterStrong from RowFooter
                    / font = fonts('StrongFootFont')  just=left asis=on protectspecialchars=off;

                    class RowFooterStrongFixed from RowFooterStrong
                    / font = fonts('FixedStrongFootFont')  just=left asis=on protectspecialchars=off;

                    class SystemFooter from TitlesAndFooters / asis=on
                            protectspecialchars=off just=left;
        end;
    run;
    quit;

    %Mend utl_pdflan100;

    %utl_pdflan100;


    %Macro Tut_Sly
    (
     stop=52,
     L1=' ',  L2=' ', L3=' ', L4=' ', L5=' ', L6=' ', L7=' ', L8=' ', L9=' ',
     L10=' ', L11=' ',
     L12=' ', L13=' ', L14=' ', L15=' ', L16=' ', L17=' ', L18=' ', L19=' ',
     L20=' ', L21=' ',
     L22=' ', L23=' ', L24=' ', L25=' ', L26=' ', L27=' ', L28=' ', L29=' ', L30=' ', L31=' ', L32=' ',
     L33=' ', L34=' ', L35=' ', L36=' ', L37=' ', L38=' ', L39=' ', L40=' ', L41=' ', L42=' ', L43=' ',
     L44=' ', L45=' ', L46=' ', L47=' ', L48=' ', L49=' ', L50=' ', L51=' ', L52=' '
     )/ des="SAS Slides all argument values need to be single quoted";

    /* creating slides for a presentation */
    /* up to 32 lines */
    /* backtic ` is converted to a single quote  */
    /* | is converted to a , */

    Data _OneLyn1st(rename=t=title);

    Length t $255;
     t=resolve(translate(&L1,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L2,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L3,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L4,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L5,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L6,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L7,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L8,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
     t=resolve(translate(&L9,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L10,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L11,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L12,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L13,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L14,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L15,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L16,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L17,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L18,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L19,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L20,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L21,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L22,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L23,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L24,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L25,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L26,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L27,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L28,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L29,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L30,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L31,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L32,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L33,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L34,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L35,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L36,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L37,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L38,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L39,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L41,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L42,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L43,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L44,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L45,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L46,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L47,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L48,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L50,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L51,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu
    t=resolve(translate(&L52,"'","`"));t=translate(t,",","|");t=translate(t,";","~");t=translate(t,'%',"#");t=translate(t,'&',"@");Outpu

    run;quit;

    /*  %let l7='^S={font_size=25pt just=c cellwidth=100pct}Premium Dollars';  */

    options label;
    %if &stop=7 %then %do;
       data _null_;
          tyt=scan(&l7,2,'}');
          call symputx("tyt",tyt);
       run;
       ods pdf bookmarkgen=on bookmarklist=show;
       ods proclabel="&tyt";run;quit;
    %end;
    %else %do;
       ods proclabel="Title";run;quit;
    %end;


    data _onelyn;
      set _onelyn1st(obs=%eval(&stop + 1));
      if not (left(title) =:  '^') then do;
         pre=upcase(scan(left(title),1,' '));
         idx=index(left(title),' ');
         title=substr(title,idx+1);
      end;
      put title;
    run;

    * display the slide ;
    title;
    footnote;

    proc report data=_OneLyn nowd  style=utl_ymrlan100;
    col title;
    define title / display ' ';
    run;
    quit;

    %Mend Tut_Sly;

    %macro utlfkil
        (
        utlfkil
        ) / des="delete an external file";


        /*-------------------------------------------------*\
        |                                                   |
        |  Delete an external file                          |
        |   From SAS macro guide                                                |
        |  Sample invocations                               |
        |                                                   |
        |  WIN95                                            |
        |  %utlfkil(c:\dat\utlfkil.sas);                    |
        |                                                   |
        |                                                   |
        |  Solaris 2.5                                      |
        |  %utlfkil(/home/deangel/delete.dat);              |
        |                                                   |
        |                                                   |
        |  Roger DeAngelis                                  |
        |                                                   |
        \*-------------------------------------------------*/

        %local urc;

        /*-------------------------------------------------*\
        | Open file   -- assign file reference              |
        \*-------------------------------------------------*/

        %let urc = %sysfunc(filename(fname,%quote(&utlfkil)));

        /*-------------------------------------------------*\
        | Delete file if it exits                           |
        \*-------------------------------------------------*/

        %if &urc = 0 and %sysfunc(fexist(&fname)) %then
            %let urc = %sysfunc(fdelete(&fname));

        /*-------------------------------------------------*\
        | Close file  -- deassign file reference            |
        \*-------------------------------------------------*/

        %let urc = %sysfunc(filename(fname,''));

      run;

    %mend utlfkil;


    %macro utl_boxpdf2ppt(inp=&outpdf001,out=&outppt001)/des="www.boxoft.con pdf to ppt";
      data _null_;
        cmd=catt("&pdf2ppt",' "',"&inp", '"',' "',"&out",'"');
        put cmd;
        call system(cmd);
      run;
    %mend utl_boxpdf2ppt;

    %MACRO greenbar ;
       DEFINE _row / order COMPUTED NOPRINT ;
       COMPUTE _row;
          nobs+1;
          _row = nobs;
          IF (MOD( _row,2 )=0) THEN
             CALL DEFINE( _ROW_,'STYLE',"STYLE={BACKGROUND=graydd}" );
       ENDCOMP;
    %MEND greenbar;

    %macro pdfbeg(rules=all,frame=box,pdf=);
        %*utlnopts;
        title;
        footnote;
        options orientation=landscape validvarname=v7;
        ods listing close;
        ods pdf close;
        ods path work.templat(update) sasuser.templat(update) sashelp.tmplmst(read);
        %utlfkil(&outpdf);
        ods noptitle;
        ods escapechar='^';
        ods listing close;
        ods graphics on / width=10in  height=7in ;
        ods pdf file="&pdf" style=utl_pdflan100 notoc ;
        run;quit;
    %mend pdfbeg;

    %macro codebegin;
      options orientation=landscape lrecl=384;
      data _null_;
      length lyn $384;
       input;
       lyn=strip(_infile_);
       file print;
       put lyn "^{newline}" @;
       *call execute(_infile_);
    %mend codebegin;


    %macro pdfend;
       ods graphics off;
       ods pdf close;
       ods listing;
       options ls=171 ps=66;
       %*utlopts;
       run;quit;
    %mend pdfend;

    *_                _
    | |__   ___  __ _(_)_ __
    | '_ \ / _ \/ _` | | '_ \
    | |_) |  __/ (_| | | | | |
    |_.__/ \___|\__, |_|_| |_|
                |___/
     _ __   ___  _ __ _ __ ___   __ _| (_)_______
    | '_ \ / _ \| '__| '_ ` _ \ / _` | | |_  / _ \
    | | | | (_) | |  | | | | | | (_| | | |/ /  __/
    |_| |_|\___/|_|  |_| |_| |_|\__,_|_|_/___\___|
    ;

    * the input looks like this;


    /*
    TAJ.TAJ_SIMULATE total obs=500 12 Months
                                                                 PAY
     ID  AGE  SMOKER  CARBS  GENDER  T1  T2  T3 ..T12     _1   _2   _3 .. _12
      1   34     1     -10      0     1   2   3 .. 12    783  808  796 .. 795
      2   29     1     -11      0     1   2   3 .. 12    817  816  833 .. 747
      3   40     0      -9      0     1   2   3 .. 12    820  813  793 .. 837
      4   38     0     -11      0     1   2   3 .. 12    786  738  706 .. 796
      5   27     1     -12      1     1   2   3 .. 12    709  796  819 .. 817
    ...
    500   37     1     -9       0     1   2   3 .. 12    719  795  829 .. 818
    */

    * lets normalize;

    proc transpose data=taj.taj_simulate out=&pgm._simNrm(rename=(_name_=mthc col1=pay));
    by id age smoker carbs gender;
    var _1-_12;
    run;quit;

    data taj.taj_simNrm(label="Normalized version of original input dataset created by &pgmloc./&pgm..sas");
       set &pgm._simNrm;
       mth=input(substr(mthc,2),3.);
       drop mthc;
    run;quit;

    /*
    p to 40 obs TAJ.TAJ_SIMNRM total obs=6,000
    Obs    ID    AGE    SMOKER    CARBS    GENDER    PAY    MTH
      1     1     34       1       -10        0      783      1
      2     1     34       1       -10        0      808      2
      3     1     34       1       -10        0      796      3
      4     1     34       1       -10        0      791      4
      5     1     34       1       -10        0      793      5
    ...
    */

    *    _ _     _
     ___| (_) __| | ___  ___
    / __| | |/ _` |/ _ \/ __|
    \__ \ | | (_| |  __/\__ \
    |___/_|_|\__,_|\___||___/
    ;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl0000.pdf);
    %Tut_Sly
       (
        stop=14
        ,L7 ='^S={font_size=30pt just=c &w}Trajectory of Payments for Food and Liesure'
        ,L9 ='^S={font_size=25pt just=c &w}Monthly Food and Leisure Costs'
        ,L10='^S={font_size=25pt just=c &w}January through December Fake Data'
        ,L13 ='^S={font_size=25pt just=c &w}SAS Proc Traj by Dr Jones'
        ,L14 ='^S={font_size=25pt just=c &w}https://www.andrew.cmu.edu/user/bjones/'
       );
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1100.pdf);
    proc sgplot data=taj.taj_simNrm;
    title "Slide 1010 Overall 12 Month Histogram of Payments" ;
    label pay="Payments Food and Leisure";
    histogram pay/binwidth=5;
    yaxis grid offsetmax=.05;
    xaxis grid;
    run;quit;
    %pdfend;

    * percent of total pay in the top 5% by month;
    * since we have exactly 500 in each month the top 10% will at 450 and above;
    proc sort data=taj.taj_simNrm out=taj_simNrmSrt;
     by mth pay;
    run;quit;
    data taj.taj_simNrmSum;
      retain cnt paySum payTot 0;
      set taj_simNrmSrt(keep=mth pay);
      by mth;
      cnt=cnt+1;
      payTot=sum(payTot,pay);
      if cnt>475 then paySum=sum(paySum,pay);
      if last.mth then do;
         payPct=100*paySum/payTot;
         cnt5Pct=25;
         output;
         cnt=0;
         paySum=0;
         payTot=0;
      end;
    run;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1200.pdf);
    proc report data=taj.taj_simNrmSum missing nowd list split="#";
       cols ("Figure 1200 Percent of Monthly Payments in the Top 5 Percent by Month"
    mth cnt payTot cnt5pct paySum payPct) _row;
    DEFINE  MTH     / display     center "Month" ;
    DEFINE  cnt     / display     center "Count" ;
    DEFINE  payTot  / display FORMAT= dollar9.   center "Total" ;
    DEFINE  cnt5pct / display     center "Count#5%" ;
    DEFINE  paySum  / display FORMAT= dollar9.   center "Pay#5%" ;
    DEFINE  payPct  / display FORMAT= 5.1        center "Percent#of#Total" ;
    %greenbar;
    run;quit;
    %pdfend;

    *     _           _
      ___| |_   _ ___| |_ ___ _ __
     / __| | | | / __| __/ _ \ '__|
    | (__| | |_| \__ \ ||  __/ |
     \___|_|\__,_|___/\__\___|_|
    ;

    * all data;
    proc fastclus data=taj_simNrmSrt out=taj.&pgm._cusAll maxiter=10 maxc=3;
    var pay;
    run;quit;

    /*
                               RMS Std
    Cluster     Frequency    Deviation
    ------------------------------------
       1             1632      23.7124
       2             2940      16.9074
       3             1428      25.2108
    */

    data taj.&pgm._cusAllx;
       set taj.&pgm._cusAll;
       select (cluster);
         when (1) clus1=pay;
         when (2) clus2=pay;
         when (3) clus3=pay;
       end;
       keep clus1-clus3 cluster pay;
    run;quit;

    proc sort data=taj.&pgm._cusAllx;
    by cluster pay;
    run;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1300.pdf);
    proc sgplot data=taj.&pgm._cusAllx;
    title1 "Figure 1300 Overall Clusters";
    title2 "All data";
    label clus1="Payments";
    histogram clus1/binwidth= 5 transparency=.8;
    histogram clus2/binwidth= 5 transparency=.6;
    histogram clus3/binwidth= 5 transparency=.4;
    run;quit;
    %pdfend;

    * cluster trajectories;
    proc summary data=taj.&pgm._cusAll nway;
    class mth cluster;
    var pay;
    output out=taj.&pgm._cusAllSum mean=;
    run;quit;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1400.pdf);
    proc sgplot data=taj.&pgm._cusAllSum ;
    title "Figure 1400 Trajectory of 3 Clusters";
    format pay dollar9.;
    label pay = "Payments";
    label mth="Month";
    series x=mth y=pay / group=cluster lineattrs=(pattern=solid thickness=2pt)
    datalabel=pay datalabelattrs=(size=12);
    xaxis  grid  offsetmin=.05 offsetmax=.15 values=(1 to 12 by 1)
    /*valueattrs=(size=12)*/ grid offsetmin=.05 offsetmax=.05;
    yaxis  grid  offsetmin=.05 offsetmax=.05;
    run;quit;
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1500.pdf);
    %Tut_Sly
       (
        stop=21
    ,L1    ='&v Figure 1500 Adjacent Months show the Strongest Correlation'
    ,L2    ='&v   Variable Correlations (Spearman)                '
    ,L3    ='&v   Month       Correlated    Correlation    Number '
    ,L4    ='&v   Variable    With Month        Coef       of Obs '
    ,L6    ='&v      7           6              0.63        500   '
    ,L7    ='&v      8           6              0.61        500   '
    ,L8    ='&v      6           5              0.61        500   '
    ,L9    ='&v      6           4              0.60        500   '
    ,L10   ='&v      4           3              0.59        500   '
    ,L11   ='&v      9           8              0.58        500   '
    ,L12   ='&v      8           7              0.58        500   '
    ,L13   ='&v      5           3              0.57        500   '
    ,L14   ='&v      4           2              0.57        500   '
    ,L15   ='&v      6           3              0.57        500   '
    ,L16   ='&v      5           4              0.56        500   '
    ,L17   ='&v      11          10             0.56        500   '
    ,L18   ='&v      10          8              0.55        500   '
    ,L19   ='&v      11          9              0.52        500   '
    ,L20   ='&v      10          9              0.52        500   '
    ,L21   ='&v      12          11             0.52        500   '
    );
    %pdfend;

    *                    _      _
     _ __ ___   ___   __| | ___| |
    | '_ ` _ \ / _ \ / _` |/ _ \ |
    | | | | | | (_) | (_| |  __/ |
    |_| |_| |_|\___/ \__,_|\___|_|
    ;

    title;
    footnote;
    %utl_pdflan100(fixedfont=11pt);
    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1510.pdf);
    %codebegin;
    cards4;

    *;
    * PROC TRAJ MULTIPLE MODELS;
    *;

    %macro cmmi_mdlchk(mdl);

    %let cmpMdl=%sysfunc(compress(&mdl));

    proc traj data = taj.taj_simulate
           outplot =   taj.taj_mdlPlot12_&cmpMdl
           outest  =    taj.taj_mdlEst12_&cmpMdl
           outstat =   taj.taj_mdlStat12_&cmpMdl
               out = taj.taj_mdlDetail12_&cmpMdl ci95M;
      model order&cmpmdl;
      id id;
      var _1-_12 ;
      risk  smoker carbs ;
      indep t1-t12;
      order &mdl;
      min 600;
      max 1000;
      model cnorm;
    run;quit;

    %mend cmmi_mdlchk;

    %*cmmi_mdlchk(1 1    );
    %*cmmi_mdlchk(1 1 1  );
    %*cmmi_mdlchk(2 1 1 1);
    %*cmmi_mdlchk(1 1 1 1);
    %*cmmi_mdlchk(1 1 2  );
    %*cmmi_mdlchk(1 2 1  );
    %*cmmi_mdlchk(1 2 2  );
    %*cmmi_mdlchk(2 1 1  );
    %*cmmi_mdlchk(2 1 2  );
    %*cmmi_mdlchk(2 2 1  );
    %*cmmi_mdlchk(2 2 2  );
    %*cmmi_mdlchk(2 2 2 2);
    ;;;;
    run;quit;
    %pdfend;
    %utl_pdflan100;  * reset;

    %macro cmmi_mdlchk(mdl);

    %let cmpMdl=%sysfunc(compress(&mdl));

    proc traj data = taj.taj_simulate
           outplot =   taj.taj_mdlPlot12_&cmpMdl
           outest  =    taj.taj_mdlEst12_&cmpMdl
           outstat =   taj.taj_mdlStat12_&cmpMdl
               out = taj.taj_mdlDetail12_&cmpMdl ci95M;
      model order&cmpmdl;
      id id;
      var _1-_12 ;
      risk  smoker carbs ;
      indep t1-t12;
      order &mdl;
      min 600;
      max 1000;
      model cnorm;
    run;quit;

    %mend cmmi_mdlchk;

    %cmmi_mdlchk(1 1    );
    %cmmi_mdlchk(1 1 1  );
    %cmmi_mdlchk(2 1 1 1);
    %cmmi_mdlchk(1 1 1 1);
    %cmmi_mdlchk(1 1 2  );
    %cmmi_mdlchk(1 2 1  );
    %cmmi_mdlchk(1 2 2  );
    %cmmi_mdlchk(2 1 1  );
    %cmmi_mdlchk(2 1 2  );
    %cmmi_mdlchk(2 2 1  );
    %cmmi_mdlchk(2 2 2  );
    %cmmi_mdlchk(2 2 2 2);
    ;;;;
    run;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1550.pdf);
    %Tut_Sly
       (
        stop=38
    ,L2   ='&x Figure 1550 12 Month Food and Leisure Payments 211 Model'
    ,L4   ='&x                         Model 211 Maximum Likelihood Estimates          '
    ,L5   ='&x                           Model: Censored Normal (CNORM)                '
    ,L7   ='&x                                    Standard       T for H0:             '
    ,L8   ='&x  Group   Parameter    Estimate        Error     Parameter=0   Prob >  |T|'
    ,L10   ='&x  1       Intercept   780.04984      4.27908         182.294       0.0000'
    ,L11   ='&x          Linear       -8.93067      1.44128          -6.196       0.0000'
    ,L12   ='&x          Quadratic     0.50581      0.10693           4.730       0.0000'
    ,L14   ='&x  2       Intercept   794.65186      1.70723         465.463       0.0000'
    ,L15   ='&x          Linear       -0.65778      0.22172          -2.967       0.0030'
    ,L17   ='&x  3       Intercept   841.05985      2.37632         353.934       0.0000'
    ,L18   ='&x          Linear       -1.25020      0.28762          -4.347       0.0000'
    ,L20   ='&x          Sigma        36.55546      0.34009         107.487       0.0000'
    ,L23   ='&x  1       Constant     (0.00000)      .                 .           .    '
    ,L25   ='&x  2       Constant      8.41491      1.17340           7.171       0.0000'
    ,L26   ='&x          SMOKER        1.04682      0.32543           3.217       0.0013'
    ,L27   ='&x          CARBS         0.70553      0.10055           7.017       0.0000'
    ,L29   ='&x  3       Constant     14.41983      1.44100          10.007       0.0000'
    ,L30   ='&x          SMOKER        2.06856      0.41146           5.027       0.0000'
    ,L31   ='&x          CARBS         1.47508      0.13837          10.660       0.0000'
    ,L33   ='&x  BIC=-30462.80 (N=6000)  BIC=-30445.40 (N=500)  AIC=-30415.90  L=-30401 '
    ,L35   ='&x  Group membership'
    ,L36   ='&x  1       (#)    20.95'
    ,L37   ='&x  2       (#)    50.16'
    ,L38   ='&x  3       (#)    28.89'
    );
    %pdfend;

    *              _     _             _
     _ __ ___  ___(_) __| |_   _  __ _| |___
    | '__/ _ \/ __| |/ _` | | | |/ _` | / __|
    | | |  __/\__ \ | (_| | |_| | (_| | \__ \
    |_|  \___||___/_|\__,_|\__,_|\__,_|_|___/
    ;

    /* inputs
    taj.taj_mdlDetail12_211
    taj.taj_mdlPlot12_211;
    */

    proc sort data=taj.taj_mdlDetail12_211 out=&pgm._detSrt noequals;
      by group id;
    run;quit;

    proc transpose data=&pgm._detSrt out=&pgm._detXpo;
      by group id;
      var _1-_12;
    run;quit;

    proc transpose data=taj.taj_mdlPlot12_211 out=&pgm._pltXpo;
      by t;
      var pred:;
    run;quit;

    proc sql;
      create
        table &pgm._res as
      select
        l.group
       ,r.t + normal(1234)/8 as t
       ,l.col1 as raw
       ,r.col1 as est
       ,r.col1 - l.col1 as resid
      from
        &pgm._detXpo as l left join &pgm._pltXpo as r
      on
       input(substr(l._name_,2),3.) = r.t and
       l.group                      = input(substr(r._name_,5),3.)
    ;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1555.pdf);
    proc sgplot data=&pgm._res;
    title "Figure 1555 Time jittered Residual Plot for Quadratic and Two Linear Model(211)";
    label resid="Residual";
    label t="Jittered Month";
    scatter x=t y=resid;
    xaxis grid values=(1 to 12 by 1) offsetmin=.1 offsetmax=.1;
    yaxis grid ;
    run;quit;
    %pdfend;

    proc standard data=&pgm._res mean=0 std=1 out=&pgm._std;
      var resid;
    run;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1565.pdf);
    proc sgplot data=&pgm._std;
    title "Figure 1565 Time jittered Standardized Residual Plot for Quadratic and Two Linear Model(211)";
    label resid="Residual";
    label t="Jittered Month";
    scatter x=t y=resid;
    xaxis grid values=(1 to 12 by 1) offsetmin=.1 offsetmax=.1;
    yaxis grid ;
    run;quit;
    %pdfend;


    *_                              __            _
    | |__   __ _ _   _  ___  ___   / _| __ _  ___| |_ ___  _ __
    | '_ \ / _` | | | |/ _ \/ __| | |_ / _` |/ __| __/ _ \| '__|
    | |_) | (_| | |_| |  __/\__ \ |  _| (_| | (__| || (_) | |
    |_.__/ \__,_|\__, |\___||___/ |_|  \__,_|\___|\__\___/|_|
                 |___/
    ;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1520.pdf);
    %Tut_Sly
       (
        stop=7
        ,L3 ='^S={font_size=20pt just=c &w}Figure 1520 Calculating a Measure of Model Fit'
        ,L5 ='^S={font_size=20pt just=c &w}Bayesian Information Criterion(BIC)'
        ,L6 ='^S={font_size=20pt just=c &w}Relative Goodness of fit against the Null Model'
        ,L7 ='^S={font_size=20pt just=c &w}BIC is preferred measure when not forcasting'
        ,L8 ='^S={font_size=20pt just=c &w}Bays factor = log(2* (BICi - BIC Null Model))'
       );
    %pdfend;


    %utl_pdflan100(fixedfont=11pt);
    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1530.pdf);
    %codebegin;
    cards4;
    data &pgm._bic2;
      * merging many model BIC staistics;
      merge
        taj.taj_mdlEst12_11   (keep=_BIC2_ obs=1 rename=_bic2_=bicnull)
        taj.taj_mdlEst12_111  (keep=_BIC2_ obs=1 rename=_bic2_=bic111 )
        taj.taj_mdlEst12_1111 (keep=_BIC2_ obs=1 rename=_bic2_=bic1111)
        taj.taj_mdlEst12_2111 (keep=_BIC2_ obs=1 rename=_bic2_=bic2111)
        taj.taj_mdlEst12_112  (keep=_BIC2_ obs=1 rename=_bic2_=bic112 )
        taj.taj_mdlEst12_121  (keep=_BIC2_ obs=1 rename=_bic2_=bic121 )
        taj.taj_mdlEst12_122  (keep=_BIC2_ obs=1 rename=_bic2_=bic122 )
        taj.taj_mdlEst12_211  (keep=_BIC2_ obs=1 rename=_bic2_=bic211 )
        taj.taj_mdlEst12_212  (keep=_BIC2_ obs=1 rename=_bic2_=bic212 )
        taj.taj_mdlEst12_221  (keep=_BIC2_ obs=1 rename=_bic2_=bic221 )
        taj.taj_mdlEst12_222  (keep=_BIC2_ obs=1 rename=_bic2_=bic222 )
        taj.taj_mdlEst12_2222 (keep=_BIC2_ obs=1 rename=_bic2_=bic2222)
       ;
    run;quit;
    ;;;;
    run;quit;
    %pdfend;
    %utl_pdflan100;


    %utl_pdflan100(fixedfont=11pt);
    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1540.pdf);
    %codebegin;
    cards4;
    data taj.&pgm._bicfits;
      set &pgm._bic2;
      * Improvements from null(two linear) Baysian Factor ;
      fit111   =  log(2 * (bic111  - bicnull));
      fit1111  =  log(2 * (bic1111 - bicnull));
      fit2111  =  log(2 * (bic2111 - bicnull));
      fit112   =  log(2 * (bic112  - bicnull));
      fit121   =  log(2 * (bic121  - bicnull));
      fit122   =  log(2 * (bic122  - bicnull));
      fit211   =  log(2 * (bic211  - bicnull));
      fit212   =  log(2 * (bic212  - bicnull));
      fit221   =  log(2 * (bic221  - bicnull));
      fit222   =  log(2 * (bic222  - bicnull));
      fit2222  =  log(2 * (bic2222 - bicnull));
      model=' 111  '; val=fit111  ;output;
      model=' 1111 '; val=fit1111 ;output;
      model=' 2111 '; val=fit2111 ;output;
      model=' 112  '; val=fit112  ;output;
      model=' 121  '; val=fit121  ;output;
      model=' 122  '; val=fit122  ;output;
      model=' 211  '; val=fit211  ;output;
      model=' 212  '; val=fit212  ;output;
      model=' 221  '; val=fit221  ;output;
      model=' 222  '; val=fit222  ;output;
      model=' 2222 '; val=fit2222 ;output;
      keep model val;
    run;quit;
    ;;;;
    run;quit;
    %pdfend;
    %utl_pdflan100;


    proc sort data=taj.&pgm._bicfits out=taj.&pgm._bicfitsrt;
     by val;
    run;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1700.pdf);
    title1 "Figure 1700 Comparison of Models Bigger is Better";
    title2 "Three and Four Trajectory Models 1-Linear 2-Quadratic";
    proc sgplot data=taj.&pgm._bicfitsrt;
    format val 4.2;
    title "Measue of Fit Bayesian Information Factors Bigger is Better";
    label val="Log Bayesian Factor";
    vbar model / response=val datalabel;
    yaxis values=(6.2  to 6.6  by .05);
    xaxis reverse grid type=discrete discreteorder=data;
    run;quit;
    %pdfend;

    * __ _ _                   _                                 _
     / _(_) |_  __   __   ___ | |__  ___  ___ _ ____   _____  __| |
    | |_| | __| \ \ / /  / _ \| '_ \/ __|/ _ \ '__\ \ / / _ \/ _` |
    |  _| | |_   \ V /  | (_) | |_) \__ \  __/ |   \ V /  __/ (_| |
    |_| |_|\__|   \_/    \___/|_.__/|___/\___|_|    \_/ \___|\__,_|
    ;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1800.pdf);
    %Tut_Sly
       (
        stop=5
        ,L3 ='^S={font_size=20pt just=c &w}Figure 1800 Fit Analysis and Residuals'
        ,L5 ='^S={font_size=20pt just=c &w}Model 211 One Quadratic Two Linear '
       );
    %pdfend;

    * model 211;
    proc transpose data=taj.taj_mdlPlot12_211 out=&pgm._mdlPlot12_211(rename=(_name_=grp col1=pay));
    by t;
    var pred1 pred2 pred3 avg1 avg2 avg3;
    run;quit;
    proc sort data=&pgm._mdlPlot12_211  out=taj.&pgm._mdlPlot12_211plt;
    by t;
    run;quit;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl1900.pdf);
    proc sgplot data=taj.&pgm._mdlPlot12_211plt  noautolegend;
    title1 "Figure 1900 Model 211 Best Fit Trajectories Payments";
    format pay dollar12.;
    label t="Month";
    Label grp="Group";
    Label Pay="Pay";
    series x=t y=pay / group=grp lineattrs=(pattern=solid thickness=2pt)
    datalabel=pay datalabelattrs=(size=10);
    xaxis  values=(1 to 12 by 1) valueattrs=(size=12) grid offsetmin=.05 offsetmax=.05;
    yaxis  grid  offsetmin=.05 offsetmax=.05
    valueattrs=(size=12);
    run;quit;
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2000.pdf);
    proc sgplot data=taj.&pgm._mdlPlot12_211plt  noautolegend;
    title1 "Figure 2000 Model 2111 Best Fit Trajectories Payments";
    format pay dollar12.;
    label t="Month";
    Label grp="Group";
    Label Pay="Pay";
    series x=t y=pay / group=grp lineattrs=(pattern=solid thickness=2pt)
    datalabel=pay datalabelattrs=(size=10);
    xaxis  values=(1 to 12 by 1) valueattrs=(size=12) grid offsetmin=.05 offsetmax=.05;
    yaxis  grid  offsetmin=.05 offsetmax=.05
    valueattrs=(size=12);
    run;quit;
    %pdfend;

    *          _                _               _  __
     _ __ ___ (_)___ ___    ___| | __ _ ___ ___(_)/ _|_   _
    | '_ ` _ \| / __/ __|  / __| |/ _` / __/ __| | |_| | | |
    | | | | | | \__ \__ \ | (__| | (_| \__ \__ \ |  _| |_| |
    |_| |_| |_|_|___/___/  \___|_|\__,_|___/___/_|_|  \__, |
                                                      |___/
    ;

    * probabilites of each of the four trajectories;
    data taj.&pgm._prbmz;
       set
        taj.taj_mdlDetail12_2111(keep=grp1prb grp2prb grp3prb grp4prb group in=N)
        taj.taj_mdlDetail12_211(keep=grp1prb grp2prb grp3prb group in=Y);
        if n then fro="2111";
        else fro="211";
        select ;
          when (group=1 and fro='2111') do; typ="1. Lowest    ";val=GRP1PRB;output;end;
          when (group=2 and fro='2111') do; typ="2. Low";val=GRP2PRB;output;end;
          when (group=3 and fro='2111') do; typ="3. High";val=GRP3PRB;output;end;
          when (group=4 and fro='2111') do; typ="4. Highest";val=GRP4PRB;output;end;
          when (group=1 and fro='211')  do; typ="1. Low";val=GRP1PRB;output;end;
          when (group=2 and fro='211')  do; typ="2. Moderate";val=GRP2PRB;output;end;
          when (group=3 and fro='211')  do; typ="3. High";val=GRP3PRB;output;end;
        end;
        keep fro group typ val;
    run;quit;
    ods trace on;
    ods exclude all;
    ods output summary=taj.&pgm._prbsum(drop=_: variable);;
    proc means data=taj.&pgm._prbmz missing stackodsoutput mean;
    class fro typ;
    var val;
    run;quit;
    ods select all;
    ods trace off;
    %utl_gather(taj.&pgm._prbsum,varx,valx,fro typ,taj.&pgm._prbxpo,valformat=9.);
    proc transpose data=taj.&pgm._prbxpo out=taj.&pgm._prbxxo;
    by fro typ;
    id varx;
    var valx;
    run;quit;

    /*
     TAJ.TAJ_210MDL_PRBXXO total obs=4 40 obs printed
                                 LOG0_     LOG0_     LOG0_     LOG0_
     Obs      typ      _NAME_    0NObs     0Mean     MNObs     MMean
      1     GRP1PRB     valx      8073    0.95443    16070    0.85369
      2     GRP2PRB     valx      6180    0.89093    18036    0.78203
      3     GRP3PRB     valx     28294    0.89986    14835    0.81451
      4     GRP4PRB     valx     28326    0.93037    21932    0.90139
    */



    options orientation=landscape;
    ods escapechah='^';
    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2100.pdf);
     proc report data=taj.&pgm._prbxxo(drop=_:) nowd missing split='#' style(header)={font_weight=bold};  ;
     COLUMN  ("^S={ just=l font_size=15pt font_face=arial}
    Figure 2100 Classification seems a little more Accurate for the 211 model ^{newline}
    Analysis will proceed wit the 211 Model (Quadratic and Two Linear)  ^{newline}^{newline}"
         fro  ("Classification Probabilities" typ nobs mean));
     DEFINE  fro / order    left "^S={just=left} Model" ;
     DEFINE  typ / display    left "^S={just=left}Trajectory" ;
     DEFINE  Nobs / "^S={just=center}Frequency"      center ;
     DEFINE  Mean / display FORMAT= 5.2      center "^S={just=center}Probability" ;
     break after fro / skip;
     compute after fro;
       lyn="  ";
       line lyn $2.;
     endcomp;
    run;quit;
    %pdfend;


    *                    _      _       _        _
     _ __ ___   ___   __| | ___| |  ___| |_ __ _| |_ ___
    | '_ ` _ \ / _ \ / _` |/ _ \ | / __| __/ _` | __/ __|
    | | | | | | (_) | (_| |  __/ | \__ \ || (_| | |_\__ \
    |_| |_| |_|\___/ \__,_|\___|_| |___/\__\__,_|\__|___/
    ;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2200.pdf);
    %Tut_Sly
       (
        stop=18
        ,L3 ='&z.&t.Figure 2200 Proc Traj Model Options             '
        ,L5 ='&z.&t.proc traj data = taj.taj_DoaClmMdl              '
        ,L6 ='&z.&t.       outplot = taj.taj_mdlPlotm4444           '
        ,L7 ='&z.&t.       outest  = taj.taj_mdlEstm4444            '
        ,L8 ='&z.&t.       outstat = taj.taj_mdlStatm4444           '
        ,L9 ='&z.&t.           out = taj.taj_mdlDetailm4444  ci95M; '
        ,L10='&z.&t.  id bene_id;                                   '
        ,L11='&z.&t.  var _1-_12 ;                                  '
        ,L12='&z.&t.  indep t1-t12;                                 '
        ,L13='&z.&t.  risk age sexn white;                          '
       ,L14 ='&z.&t.  order 4 4 4 4;                                '
       ,L15 ='&z.&t.  min -8;                                       '
       ,L16 ='&z.&t.  max 16;                                       '
       ,L17 ='&z.&t.  model cnorm;                                  '
       ,L18 ='&z.&t.run;quit;                                       '
       );
    %pdfend;



    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2300.pdf);
    %Tut_Sly
       (
        stop=34
    ,L1    ='&v Figure 2300 12 Month Spending Quartic Trajectory Censored Normal (CNORM)'
    ,L3    ='&v                                   Standard       T for H0:             '
    ,L4    ='&v Group   Parameter    Estimate        Error     Parameter=0   Prob > |T| '
    ,L6    ='&v 1       Intercept     9.92983      0.06978         142.301       0.0000 '
    ,L7    ='&v         Linear       -5.15324      0.07270         -70.886       0.0000 '
    ,L8    ='&v         Quadratic     1.07541      0.02193          49.033       0.0000 '
    ,L9    ='&v         Cubic        -0.09287      0.00247         -37.531       0.0000 '
    ,L10   ='&v         Quartic       0.00286      0.00009          30.593       0.0000 '
    ,L12   ='&v 2       Intercept     4.99144      0.09673          51.604       0.0000 '
    ,L13   ='&v         Linear        3.44440      0.09334          36.902       0.0000 '
    ,L14   ='&v         Quadratic    -1.20220      0.02718         -44.226       0.0000 '
    ,L15   ='&v         Cubic         0.12346      0.00312          39.542       0.0000 '
    ,L16   ='&v         Quartic      -0.00408      0.00012         -33.838       0.0000 '
    ,L18   ='&v 3       Intercept     8.08606      0.04155         194.612       0.0000 '
    ,L19   ='&v         Linear       -0.73841      0.04082         -18.091       0.0000 '
    ,L20   ='&v         Quadratic     0.04575      0.01149           3.981       0.0001 '
    ,L21   ='&v         Cubic         0.00245      0.00127           1.932       0.0533 '
    ,L22   ='&v         Quartic      -0.00024      0.00005          -4.908       0.0000 '
    ,L24   ='&v 4       Intercept     5.99090      0.03727         160.763       0.0000 '
    ,L25   ='&v         Linear        1.94456      0.03580          54.318       0.0000 '
    ,L26   ='&v         Quadratic    -0.51693      0.01047         -49.379       0.0000 '
    ,L27   ='&v         Cubic         0.05200      0.00118          44.051       0.0000 '
    ,L28   ='&v         Quartic      -0.00182      0.00004         -40.386       0.0000 '
    ,L30   ='&v Group membership           '
    ,L31   ='&v 1       (%)    11.40 '
    ,L32   ='&v 2       (%)     8.99 '
    ,L33   ='&v 3       (%)    39.57 '
    ,L34   ='&v 4       (%)    40.03 '
    );
    %pdfend;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2400.pdf);
    %Tut_Sly
       (
        stop=22
    ,L1    ='&v Figure 2400 12 Month Payments Quartic Model Covariates continued      '
    ,L3    ='&v Covariates                                                             '
    ,L5    ='&v 1       Constant     (0.00000)      .                 .           .    '
    ,L7    ='&v 2       Constant     -1.51110      0.14052         -10.753       0.0000'
    ,L8    ='&v         AGE           0.01754      0.00168          10.443       0.0000'
    ,L9    ='&v         Sexn         -0.26847      0.03775          -7.111       0.0000'
    ,L10   ='&v         White         0.02082      0.04781           0.436       0.6632'
    ,L12   ='&v 3       Constant     -1.28141      0.10357         -12.372       0.0000'
    ,L13   ='&v         AGE           0.03034      0.00123          24.768       0.0000'
    ,L14   ='&v         Sexn         -0.54964      0.02768         -19.855       0.0000'
    ,L15   ='&v         White         0.40781      0.03638          11.208       0.0000'
    ,L17   ='&v 4       Constant      2.10539      0.09289          22.666       0.0000'
    ,L18   ='&v         AGE          -0.00681      0.00113          -6.039       0.0000'
    ,L19   ='&v         Sexn         -0.57921      0.02708         -21.392       0.0000'
    ,L20   ='&v         White        -0.01461      0.03364          -0.434       0.6640'
    ,L22   ='&v BIC= -1946840 (N=850476)  BIC= -1946799 (N=70873)  AIC= -1946648  L= -1946615'
    );
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2500.pdf);
    %Tut_Sly
       (
        stop=33
    ,L1    ='&v Figure 2500 INPUT Payments Proc Tjaj ( Log of Spending)'
    ,L2    ='&v Transposed Middle Observation(35436) of TAJ.TAJ_DOACLMMDL- Obs 70,873'
    ,L4    ='&v bene_id    n8    33827648  unique beneficiary identifier'
    ,L5    ='&v age        n8    91        age'
    ,L6    ='&v sexn       n8    1         gender'
    ,L7    ='&v white      n8    1         white non-hispanic'
    ,L9    ='&v _1         N8    9.452     Payment Month of Death'
    ,L10   ='&v _2         N8    8.984     Payment 1 Month prior'
    ,L11   ='&v _3         N8    3.735     Payment 2 Months prior'
    ,L12   ='&v _4         N8    3.473     Payment 3 Months prior'
    ,L13   ='&v _5         N8    6.244     Payment 4 Months prior'
    ,L14   ='&v _6         N8    6.155     Payment 5 Months prior'
    ,L15   ='&v _7         N8    6.965     Payment 6 Months prior'
    ,L16   ='&v _8         N8    5.154     Payment 7 Months prior'
    ,L17   ='&v _9         N8    0         Payment 8 Months prior'
    ,L18   ='&v _10        N8    0         Payment 9 Months prior'
    ,L19   ='&v _11        N8    5.383     Payment 10 Months prior'
    ,L20   ='&v _12        N8    0         Payment 11 Months prior'
    ,L22   ='&v t1         N8    1         Month of Death'
    ,L23   ='&v t2         N8    2         Month_1'
    ,L24   ='&v t3         N8    3         Month_2'
    ,L25   ='&v t4         N8    4         Month_3'
    ,L26   ='&v t5         N8    5         Month_4'
    ,L27   ='&v t6         N8    6         Month_5'
    ,L28   ='&v t7         N8    7         Month_6'
    ,L29   ='&v t8         N8    8         Month_7'
    ,L30   ='&v t9         N8    9         Month_8'
    ,L31   ='&v t10        N8    10        Month_9'
    ,L32   ='&v t11        N8    11        Month_10'
    ,L33   ='&v t12        N8    12        Month_11'
    );
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2600.pdf);
    %Tut_Sly
       (
        stop=12
    ,L1    ='&v Figure 2600 OUTSTAT 12 Month Quartic Spending Model Table '
    ,L3    ='&v Trajectory Coeficiants (TAJ.TAJ_MDLSTATM4444)'
    ,L5    ='&v        Intercepts   Linear     Quadratic    Cubic      Quartic              Group_Pct'
    ,L7    ='&v Group   beta0       beta1       beta2       beta3       beta4      beta5       pi'
    ,L9    ='&v  1     9.92983    -5.15324     1.07541    -0.09287    0.0028614      .      11.4039'
    ,L10   ='&v  2     4.99144     3.44440    -1.20220     0.12346    -.0040840      .       8.9914'
    ,L11   ='&v  3     8.08606    -0.73841     0.04575     0.00245    -.0002354      .      39.5704'
    ,L12   ='&v  4     5.99090     1.94456    -0.51693     0.05200    -.0018163      .      40.0342'
    );
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2700.pdf);
    %Tut_Sly
       (
        stop=31
    ,L1    ='&v Figure 2700 OUTPLOT Proc Traj TAJ.TAJ_MDLPLOTM4444 Table Has 12 rows one per year'
    ,L3    ='&v Transposed Middle Observation(6) of TAJ.TAJ_MDLPLOTM4444 - Total Obs 12'
    ,L6    ='&v Variable              Typical'
    ,L7    ='&v Name         Type     Value     Description'
    ,L9    ='&v T             N8       6        Interval'
    ,L11   ='&v AVG1          N8       1.451    Average 1'
    ,L12   ='&v AVG2          N8       3.773    Average 2'
    ,L13   ='&v AVG3          N8       5.588    Average 3'
    ,L14   ='&v AVG4          N8       7.993    Average 4'
    ,L16   ='&v PRED1         N8       1.373    Estimate 1'
    ,L17   ='&v PRED2         N8       3.754    Estimate 2'
    ,L18   ='&v PRED3         N8       5.527    Estimate 3'
    ,L19   ='&v PRED4         N8       7.927    Estimate 4'
    ,L21   ='&v L95M1         N8       1.342    Lower 95% C.I. for Mean Traj 1'
    ,L22   ='&v U95M1         N8       1.404    Upper 95% C.I. for Mean Traj 1'
    ,L24   ='&v L95M2         N8       3.665    Lower 95% C.I. for Mean Traj 2'
    ,L25   ='&v U95M2         N8       3.842    Upper 95% C.I. for Mean Traj 2'
    ,L27   ='&v L95M3         N8       5.501    Lower 95% C.I. for Mean Traj 3'
    ,L28   ='&v U95M3         N8       5.552    Upper 95% C.I. for Mean Traj 3'
    ,L30   ='&v L95M4         N8       7.909    Lower 95% C.I. for Mean Traj 4'
    ,L31   ='&v U95M4         N8       7.945    Upper 95% C.I. for Mean Traj 4'
    );
    %pdfend;


    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2800.pdf);
    %Tut_Sly
       (
        stop=41
    ,L1    ='&x Figure 2800 OUT Spending Transpose Proc Traj OUT Table'
    ,L2    ='&x Middle Observation(35436) of OUT table taj.taj_mdlDetailm4444-Total Obs 70,873'
    ,L4    ='&x Variable     Type     Value        Description'
    ,L6    ='&x bene_id       N8      33827648     bene_id'
    ,L7    ='&x group         N8      2            group'
    ,L8    ='&x age           N8      91           age'
    ,L9    ='&x sexn          N8      1            gender 1=Female'
    ,L10   ='&x white         N8      1            white non_hispanic'
    ,L12   ='&x _1            N8      9.452        Payment Month of Death'
    ,L13   ='&x _2            N8      8.984        Payment 1 Month prior'
    ,L14   ='&x _3            N8      3.735        Payment 2 Months prior'
    ,L15   ='&x _4            N8      3.473        Payment 3 Months prior'
    ,L16   ='&x _5            N8      6.244        Payment 4 Months prior'
    ,L17   ='&x _6            N8      6.155        Payment 5 Months prior'
    ,L18   ='&x _7            N8      6.965        Payment 6 Months prior'
    ,L19   ='&x _8            N8      5.154        Payment 7 Months prior'
    ,L20   ='&x _9            N8      0            Payment 8 Months prior'
    ,L21   ='&x _10           N8      0            Payment 9 Months prior'
    ,L22   ='&x _11           N8      5.383        Payment 10 Months prior'
    ,L23   ='&x _12           N8      0            Payment 11 Months prior'
    ,L25   ='&x t1            N8      1            Month of Death'
    ,L26   ='&x t2            N8      2            Month_1'
    ,L27   ='&x t3            N8      3            Month_2'
    ,L28   ='&x t4            N8      4            Month_3'
    ,L29   ='&x t5            N8      5            Month_4'
    ,L30   ='&x t6            N8      6            Month_5'
    ,L31   ='&x t7            N8      7            Month_6'
    ,L32   ='&x t8            N8      8            Month_7'
    ,L33   ='&x t9            N8      9            Month_8'
    ,L34   ='&x t10           N8      10           Month_9'
    ,L35   ='&x t11           N8      11           Month_10'
    ,L36   ='&x t12           N8      12           Month_11'
    ,L38   ='&x GRP1PRB       N8      0.000        Group 1 Probability'
    ,L39   ='&x GRP2PRB       N8      0.748        Group 2 Probability'
    ,L40   ='&x GRP3PRB       N8      0.251        Group 3 Probability'
    ,L41   ='&x GRP4PRB       N8      4.28E-7      Group 4 Probability'
    );
    %pdfend;

    %pdfbeg(pdf=d:/taj/pdf/&pgm._tbl2900.pdf);
    %Tut_Sly
       (
        stop=46
    ,L1   ='&x Figure 2900 OUTEST Proc Traj OUT Table'
    ,L2   ='&x OUTEST Middle Observation(17) of taj.taj_mdlEstm4444-Total Obs 35'
    ,L4   ='&x VARIABLE    TYPE      TYPICAL VALUE'
    ,L5   ='&x _MODEL_      C8        CNORM'
    ,L6   ='&x _NAME_       C32       QUARTIC'
    ,L7   ='&x _LOGLIK_     N8        -1946614.659'
    ,L9   ='&x _BIC1_       N8       -1946798.942'
    ,L10  ='&x _BIC2_       N8       -1946839.943'
    ,L11  ='&x _AIC_        N8       -1946647.659'
    ,L12  ='&x _CONVERGE_   N8       4           '
    ,L13  ='&x _TYPE_       C8       COV         '
    ,L14  ='&x INTERC1      N8       -5.352338E-8'
    ,L15  ='&x LINEAR1      N8       3.3178097E-8'
    ,L16  ='&x QUADRA1      N8       -1.022956E-8'
    ,L17  ='&x CUBIC1       N8       1.1473296E-9'
    ,L18  ='&x QUARTI1      N8       -4.27942E-11'
    ,L19  ='&x INTERC2      N8       -4.527406E-7'
    ,L20  ='&x LINEAR2      N8       5.1836362E-7'
    ,L21  ='&x QUADRA2      N8       -1.684159E-7'
    ,L22  ='&x CUBIC2       N8       1.9887737E-8'
    ,L23  ='&x QUARTI2      N8       -7.65807E-10'
    ,L24  ='&x INTERC3      N8       1.4941047E-6'
    ,L25  ='&x LINEAR3      N8       -1.69301E-6 '
    ,L26  ='&x QUADRA3      N8       5.2513926E-7'
    ,L27  ='&x CUBIC3       N8       -6.036748E-8'
    ,L28  ='&x QUARTI3      N8       2.3016339E-9'
    ,L29  ='&x INTERC4      N8       -1.587405E-7'
    ,L30  ='&x LINEAR4      N8       1.6175198E-7'
    ,L31  ='&x QUADRA4      N8       -5.039339E-8'
    ,L32  ='&x CUBIC4       N8       5.689714E-9 '
    ,L33  ='&x QUARTI4      N8       -2.12274E-10'
    ,L34  ='&x SIGMA1       N8       -1.55326E-10'
    ,L35  ='&x CONST2       N8       -3.923857E-8'
    ,L36  ='&x AGE2         N8       8.832212E-10'
    ,L37  ='&x SEXN2        N8       -6.79816E-9 '
    ,L38  ='&x WHITE2       N8       3.6724712E-9'
    ,L39  ='&x CONST3       N8       -2.177149E-8'
    ,L40  ='&x AGE3         N8       1.912544E-10'
    ,L41  ='&x SEXN3        N8       -4.094042E-9'
    ,L42  ='&x WHITE3       N8       2.9785016E-9'
    ,L43  ='&x CONST4       N8       -4.451533E-8'
    ,L44  ='&x AGE4         N8       9.97755E-10 '
    ,L45  ='&x SEXN4        N8       -4.683381E-9'
    ,L46  ='&x WHITE4       N8       1.1910441E-8'
    );
    %pdfend;

    *     _     _                                       _ _             _
      ___| |__ | | __  _ __   ___  _ __ _ __ ___   __ _| (_)_______  __| |
     / __| '_ \| |/ / | '_ \ / _ \| '__| '_ ` _ \ / _` | | |_  / _ \/ _` |
    | (__| | | |   <  | | | | (_) | |  | | | | | | (_| | | |/ /  __/ (_| |
     \___|_| |_|_|\_\ |_| |_|\___/|_|  |_| |_| |_|\__,_|_|_/___\___|\__,_|

    see  https://github.com/rogerjdeangelis/voodoo
    ;
                    ;;;;/*'*/ *);*};*];*/;/*"*/;%mend;run;quit;%end;end;run;endcomp;%utlfix;
    * Overall trajectory of means;

    proc sql;
      create
         table &pgm._rawPlt as
      select
         mth
        ,mean(pay) as avg
      from
         taj.taj_simNrm
      group
         by mth
    ;quit;

    /*  Overall trend
    options ls=64 ps=26;
    proc plot data=&pgm._rawPlt ;
    format _numeric_ 3.;
    plot  avg*mth="*";
    run;quit;
    options ls=171  ps=66;
    AVG |
    810 +
        |       Plot of Mean Pay by Month
        |    *
        |
        |
    800 + *     *
        |
        |          *
        |             *  *
        |                      *        *
    790 +                            *     *
        |                   *     *
        |
        |
        |
    780 +
        |
        --+--+--+--+--+--+--+--+--+--+--+--+-
          1  2  3  4  5  6  7  8  9 10 11 12
                         MTH
                          Histogram (All Pay)                #  Boxplot
    990+*                                                    1     0
       .*                                                    7     0
       .*                                                    9     0
       .*                                                   19     0
       .***                                                 59     |
       .******                                             111     |
       .*************                                      286     |
       .**********************                             473     |
       .***********************************                755  +-----+
    810+*********************************************      973  |     |
       .************************************************  1049  *--+--*
       .******************************************         917  +-----+
       .***************************                        592     |
       .*******************                                401     |
       .**********                                         217     |
       .****                                                88     |
       .**                                                  34     0
       .*                                                    7     0
    630+*                                                    2     0
        ----+----+----+----+----+----+----+----+----+---
        * may represent up to 22 counts
    /*
    * lets run the varification and validation macro on the normalized data;
    * add one char var voodoo requires at least one char and one numeric;
    data &pgm._vooDoo;
      retain a 'A';
      set taj.taj_simNrm;
    run;quit;
    %include "c:/oto/oto_voodoo.sas";
    %utlvdoc
        (
        libname        = work
        ,data          = &pgm._vooDoo
        ,key           = id  mth
        ,ExtrmVal      = 10
        ,UniPlot       = 1
        ,UniVar        = 1
        ,chart         = 0
        ,taball        = mth age gender smoker carbs
        ,tabone        = mth
        ,mispop        = 1
        ,dupcol        = 0
        ,unqtwo        = mth age gender smoker carbs
        ,vdocor        = 1
        ,oneone        = 0
        ,cramer        = 1
        ,optlength     = 1
        ,maxmin        = 1
        ,unichr        = 0
        ,outlier       = 1
        ,printto       = d:\taj\vdo\&data..txt
        ,Cleanup       = 1
        );
     sample output
    Variable Correlations (Spearman Strongest)
                Correlated    Correlation    Number
    Variable       With           Coef       of Obs
     PAY          CARBS         0.43731       6000
     PAY          AGE           0.15993       6000
     PAY          SMOKER        0.13536       6000
     CARBS        AGE           0.10728       6000
     MTH          PAY           0.07191       6000
    There are no missing values
     #     Variable        Unique Values
    ---    --------        -------------
      2    AGE                       31
      3    CARBS                     15
      4    GENDER                     2
      5    ID                       500
      6    MTH                       12
      7    PAY                      285
      8    SMOKER                     2
                            N
    Variable       N    Miss         Minimum         Maximum            Mean          Median         Std Dev             Sum
    ------------------------------------------------------------------------------------------------------------------------
    AGE         6000       0      19.0000000      52.0000000      37.3580000      37.0000000       5.2129037       224148.00
    CARBS       6000       0     -17.0000000      -3.0000000     -10.1140000     -10.0000000       2.3250602       -60684.00
    GENDER      6000       0               0       1.0000000       0.5180000       1.0000000       0.4997175         3108.00
    ID          6000       0       1.0000000     500.0000000     250.5000000     250.5000000     144.3493082      1503000.00
    MTH         6000       0       1.0000000      12.0000000       6.5000000       6.5000000       3.4523402        39000.00
    PAY         6000       0     627.0000000     981.0000000     794.0865000     794.0000000      47.1780526      4764519.00
    SMOKER      6000       0               0       1.0000000       0.5020000       1.0000000       0.5000377         3012.00
    ------------------------------------------------------------------------------------------------------------------------
    *
      __ _  __ _  ___
     / _` |/ _` |/ _ \
    | (_| | (_| |  __/
     \__,_|\__, |\___|
           |___/
    ;
    Variable:  AGE
    Quantiles (Definition 5)
    Level         Quantile
    100% Max          52.0
    99%               49.5
    95%               46.0
    90%               44.0
    75% Q3            41.0
    50% Median        37.0
    25% Q1            34.0
    10%               31.0
    5%                29.0
    1%                26.0
    0% Min            19.0
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
       19     2808           52     2636
       19     2807           52     2637
       19     2806           52     2638
       19     2805           52     2639
       19     2804           52     2640
                          Histogram                          #  Boxplot
     53+*                                                   12     0
       .***                                                 48     |
       .****                                                72     |
       .************                                       228     |
       .******************                                 360     |
       .***************************                        528     |
       .*****************************************          804  +-----+
       .*********************************************      888  |     |
       .************************************************   960  *--+--*
       .**************************************             744  +-----+
       .*************************                          492     |
       .************************                           468     |
       .*************                                      252     |
       .*****                                               96     |
       .*                                                   12     |
       .*                                                   12     0
       .*                                                   12     0
     19+*                                                   12     0
        ----+----+----+----+----+----+----+----+----+---
        * may represent up to 20 counts
    *               _
      ___ __ _ _ __| |__  ___
     / __/ _` | '__| '_ \/ __|
    | (_| (_| | |  | |_) \__ \
     \___\__,_|_|  |_.__/|___/
    ;
    The UNIVARIATE Procedure
    Variable:  CARBS
    Quantiles (Definition 5)
    Level         Quantile
    100% Max          -3.0
    99%               -4.0
    95%               -6.0
    90%               -7.0
    75% Q3            -9.0
    50% Median       -10.0
    25% Q1           -11.5
    10%              -13.0
    5%               -14.0
    1%               -15.0
    0% Min           -17.0
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
      -17     5340           -3     4820
      -17     5339           -3     4821
      -17     5338           -3     4822
      -17     5337           -3     4823
      -17     5336           -3     4824
                              Histogram                          #  Boxplot
       -2.5+*                                                   12     0
           .***                                                 60     0
           .****                                                84     0
       -5.5+*********                                          204     |
           .*****************                                  408     |
           .***************************                        648     |
       -8.5+************************************               864  +-----+
           .*********************************************     1080  *-----*
           .************************************************  1140  |  +  |
      -11.5+**************************                         624  +-----+
           .*****************                                  396     |
           .************                                       276     |
      -14.5+*******                                            168     |
           .*                                                   24     0
           .*                                                   12     0
      -17.5+
            ----+----+----+----+----+----+----+----+----+---
            * may represent up to 24 counts
    *
     _ __   __ _ _   _
    | '_ \ / _` | | | |
    | |_) | (_| | |_| |
    | .__/ \__,_|\__, |
    |_|          |___/
    ;
    The UNIVARIATE Procedure
    Variable:  PAY
    Quantiles (Definition 5)
    Level         Quantile
    100% Max           981
    99%                909
    95%                871
    90%                854
    75% Q3             825
    50% Median         794
    25% Q1             763
    10%                733
    5%                 717
    1%                 686
    0% Min             627
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
      627     3319          972     1813
      636     2256          974     3241
      647     5913          976     1814
      647      861          978     1345
      651     5384          981     3733
                              Histogram                          #  Boxplot
        990+*                                                    1     0
           .*                                                    7     0
           .*                                                    9     0
           .*                                                   19     0
           .***                                                 59     |
           .******                                             111     |
           .*************                                      286     |
           .**********************                             473     |
           .***********************************                755  +-----+
        810+*********************************************      973  |     |
           .************************************************  1049  *--+--*
           .******************************************         917  +-----+
           .***************************                        592     |
           .*******************                                401     |
           .**********                                         217     |
           .****                                                88     |
           .**                                                  34     0
           .*                                                    7     0
        630+*                                                    2     0
            ----+----+----+----+----+----+----+----+----+---
            * may represent up to 22 counts
    *     _     _       __       _
      ___| |__ | | __  / _| __ _| |_
     / __| '_ \| |/ / | |_ / _` | __|
    | (__| | | |   <  |  _| (_| | |_
     \___|_| |_|_|\_\ |_|  \__,_|\__|
    ;
    * lets run the varification and validation macro on the normalized data;
    * add one char var voodoo requires at least one char and one numeric;
    data &pgm._vooDooRaw;
      retain a 'A';
      set taj.taj_simulate;
    run;quit;
    %include "c:/oto/oto_voodoo.sas";
    %utlvdoc
        (
        libname        = work
        ,data          = &pgm._vooDooRaw
        ,key           = id
        ,ExtrmVal      = 10
        ,UniPlot       = 1
        ,UniVar        = 1
        ,chart         = 0
        ,taball        = _1 age gender smoker carbs
        ,tabone        = _1
        ,mispop        = 0
        ,dupcol        = 0
        ,unqtwo        = _1 _6 _12 age gender smoker carbs
        ,vdocor        = 1
        ,oneone        = 0
        ,cramer        = 0
        ,optlength     = 0
        ,maxmin        = 0
        ,unichr        = 0
        ,outlier       = 1
        ,printto       = d:\taj\vdo\&data..txt
        ,Cleanup       = 1
        );
    Month                 N
    Variable      N    Miss         Minimum         Maximum            Mean          Median         Std Dev             Sum
    -----------------------------------------------------------------------------------------------------------------------
    _1          500       0     700.0000000     981.0000000     799.1420000     785.0000000      58.5825030       399571.00  Trend rever
    _2          500       0     678.0000000     976.0000000     805.3160000     808.0000000      43.2480859       402658.00
    _3          500       0     686.0000000     930.0000000     799.5280000     800.0000000      43.7068163       399764.00
    _4          500       0     666.0000000     913.0000000     796.6880000     795.5000000      42.8709049       398344.00
    _5          500       0     672.0000000     917.0000000     793.6380000     795.0000000      45.5108056       396819.00
    _6          500       0     653.0000000     909.0000000     793.7320000     794.0000000      41.6328087       396866.00
    _7          500       0     627.0000000     936.0000000     788.7560000     792.0000000      47.4217049       394378.00
    _8          500       0     651.0000000     933.0000000     792.1260000     792.0000000      47.0195683       396063.00
    _9          500       0     647.0000000     946.0000000     787.6900000     786.0000000      47.8639720       393845.00
    _10         500       0     659.0000000     936.0000000     790.3580000     790.0000000      42.9943119       395179.00
    _11         500       0     651.0000000     968.0000000     792.1960000     793.0000000      49.6382665       396098.00
    _12         500       0     636.0000000     909.0000000     789.8680000     791.0000000      50.4258675       394934.00
    AGE         500       0      19.0000000      52.0000000      37.3580000      37.0000000       5.2176896        18679.00
    CARBS       500       0     -17.0000000      -3.0000000     -10.1140000     -10.0000000       2.3271948        -5057.00
    GENDER      500       0               0       1.0000000       0.5180000       1.0000000       0.5001763     259.0000000
    ID          500       0       1.0000000     500.0000000     250.5000000     250.5000000     144.4818328       125250.00
    SMOKER      500       0               0       1.0000000       0.5020000       1.0000000       0.5004967     251.0000000
    -----------------------------------------------------------------------------------------------------------------------
    *                      _   _       ____
     _ __ ___   ___  _ __ | |_| |__   |___ \
    | '_ ` _ \ / _ \| '_ \| __| '_ \    __) |
    | | | | | | (_) | | | | |_| | | |  / __/
    |_| |_| |_|\___/|_| |_|\__|_| |_| |_____|
    ;
    Quantiles (Definition 5)
    Level         Quantile
    100% Max         976.0
    99%              903.5
    95%              871.5
    90%              859.5
    75% Q3           833.5
    50% Median       808.0    ** median 808 (775 - 833)
    25% Q1           775.5
    10%              749.5
    5%               731.0
    1%               698.0
    0% Min           678.0
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
      678      355          907      367
      688       48          917      265
      691      188          923      404
      695      449          941      276
      698      159          976      152
                              Histogram                         #  Boxplot
        970+*                                                   1     0
           .*                                                   1     0
           .*                                                   1     0
        910+**                                                  3     |
           .****                                                8     |
           .******************                                 36     |
        850+*****************************                      58     |
           .*****************************************          81  +-----+
           .***********************************************    93  *--+--*
        790+******************************************         84  |     |
           .*******************************                    62  +-----+
           .******************                                 35     |
        730+***********                                        22     |
           .*****                                               9     |
           .***                                                 5     0
        670+*                                                   1     0
            ----+----+----+----+----+----+----+----+----+--
            * may represent up to 2 counts
    *                      _   _        __
     _ __ ___   ___  _ __ | |_| |__    / /_
    | '_ ` _ \ / _ \| '_ \| __| '_ \  | '_ \
    | | | | | | (_) | | | | |_| | | | | (_) |
    |_| |_| |_|\___/|_| |_|\__|_| |_|  \___/
    ;
    Quantiles (Definition 5)
    Level         Quantile
    100% Max         909.0
    99%              891.0
    95%              860.0
    90%              847.5
    75% Q3           822.0
    50% Median       794.0    ** 794    (IQR 766-822)
    25% Q1           766.0
    10%              742.0
    5%               728.0
    1%               697.5
    0% Min           653.0
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
      653      320          893       21
      672        4          894      141
      673       48          897      155
      679      102          899       50
      693      434          909      107
                   Histogram              #  Boxplot
        905+*                             1     0
           .**                            4     |
           .****                          8     |
           .**                            4     |
           .*****                        10     |
        855+**********                   19     |
           .***********                  22     |
           .****************             31     |
           .*******************          37  +-----+
           .******************           36  |     |
        805+*************************    50  |     |
           .************************     47  *--+--*
           .*************************    50  |     |
           .*********************        42  |     |
           .*****************            34  +-----+
        755+*****************            33     |
           .************                 24     |
           .***********                  21     |
           .****                          8     |
           .*****                        10     |
        705+**                            4     |
           .*                             1     |
           .
           .**                            3     0
           .
        655+*                             1     0
            ----+----+----+----+----+
            * may represent up to 2 counts
    *                      _   _       _ ____
     _ __ ___   ___  _ __ | |_| |__   / |___ \
    | '_ ` _ \ / _ \| '_ \| __| '_ \  | | __) |
    | | | | | | (_) | | | | |_| | | | | |/ __/
    |_| |_| |_|\___/|_| |_|\__|_| |_| |_|_____|
    ;
    Quantiles (Definition 5)
    Level         Quantile
    100% Max         909.0
    99%              901.0
    95%              874.5
    90%              855.0
    75% Q3           822.0
    50% Median       791.0   ** 791    (IQR 758 - 822)
    25% Q1           758.5
    10%              722.0
    5%               698.5
    1%               673.5
    0% Min           636.0
    The UNIVARIATE Procedure
    Variable:  _12
            Extreme Observations
    ----Lowest----        ----Highest---
    Value      Obs        Value      Obs
      636      188          902      208
      666      445          905       58
      669      499          907      374
      672      277          909      302
      673       48          909      382
                           Histogram                      #  Boxplot
        910+***                                           6     |
           .*******                                      13     |
           .***********                                  21     |
           .*******************                          37     |
           .*****************************                58  +-----+
           .*****************************************    82  |     |
           .*************************************        74  *--+--*
        770+*****************************************    81  |     |
           .**************************                   51  +-----+
           .****************                             32     |
           .**********                                   20     |
           .********                                     16     |
           .****                                          8     |
           .
        630+*                                             1     0
            ----+----+----+----+----+----+----+----+-
            * may represent up to 2 counts
    Variable Correlations (Spearman)
    Month       Correlated    Correlation    Number    Spearman
    Variable    With Month        Coef       of Obs       P
      _7          _6            0.63447        500      0.3753
      _8          _6            0.61983        500      0.0358
      _6          _5            0.61352        500      0.5172
      _6          _4            0.60160        500      0.5172
      _4          _3            0.59525        500      0.6490
      _9          _8            0.58736        500      0.2632
      _8          _7            0.58443        500      0.0358
      _5          _3            0.57920        500      0.2956
      _4          _2            0.57605        500      0.6490
      _6          _3            0.57214        500      0.5172
      _9          _5            0.57063        500      0.2632
      _9          _6            0.56734        500      0.2632
      _5          _4            0.56633        500      0.2956
      _11         _10           0.56224        500      0.9637
      _10         _8            0.55545        500      0.8134
      _11         _9            0.52293        500      0.9637
      _10         _6            0.52240        500      0.8134
      _10         _9            0.52236        500      0.8134
      _12         _11           0.52214        500      0.3081

    Combining all pdf files in a directory

     You need to downlaod ghostscript and copy the executable
     gswin64c.exe into c:/pdf where your pdfs are located.

    INPUT
    =====

      c:/pdf

       gswin64c.exe   * ghostscript executable;

       c:/pdf/iris_page1.pdf
       c:/pdf/iris_page2.pdf
       c:/pdf/iris_page3.pdf

     EXAMLE OUTPUT  (One file with thre pages)

       c:/pdf/iris.pdf

    PROCESS
    =======

       x "cd c:/pdf";
       x 'for %s in (*.pdf) do ECHO %s >> filename.txt';
       x "gswin64c.exe -q -dNOPAUSE -sDEVICE=pdfwrite -sOutputFile=iris.pdf -dBATCH @filename.txt";

    OUTPUT
    ======

      Single file with all pds combined

       c:/pdf/iris.pdf

     *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    ods pdf file="c:/pdf/iris_page1.pdf";
    proc print data=sashelp.iris(obs=10 where=(species="Setosa"));
    run;quit;
    ods pdf close;

    ods pdf file="c:/pdf/iris_page2.pdf";
    proc print data=sashelp.iris(obs=10 where=(species="Versicolor"));
    run;quit;
    ods pdf close;

    ods pdf file="c:/pdf/iris_page3.pdf";
    proc print data=sashelp.iris(obs=10 where=(species="Virginica"));
    run;quit;
    ods pdf close;

    */

    *               _
      ___ _ __   __| |
     / _ \ '_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|
    ;
