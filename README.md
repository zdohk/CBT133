~~~~~~~~~~~~~~~~

//***FILE 133 is from Alan C. Field, and contains several of his    *   FILE 133
//*           utilities.  This file contains the following members, *   FILE 133
//*           with JCL to assemble them.                            *   FILE 133
//*                                                                 *   FILE 133
//*           Note:  Also look at CBT File 066 from Alan Field.     *   FILE 133
//*                                                                 *   FILE 133
//*           email:    alan_c_field@bluecrossmn.com                *   FILE 133
//*                                                                 *   FILE 133
//*           All this stuff now assembles cleanly on z/OS 1.13     *   FILE 133
//*           and it seems to run OK there, too.                    *   FILE 133
//*                                                                 *   FILE 133
//*           For the old versions of everything, see member ASM.   *   FILE 133
//*                                                                 *   FILE 133
//*           CLIST    - SOME CLISTS TO DEMONSTRATE THE USE OF SOME *   FILE 133
//*                      OF THE UTILITIES INCLUDED IN THIS FILE.    *   FILE 133
//*                      (in IEBUPDTE SYSIN format)                 *   FILE 133
//*                                                                 *   FILE 133
//*           CNTL     - JCL TO RUN SOME OF THE UTILITIES INCLUDED  *   FILE 133
//*                      IN THIS FILE.                              *   FILE 133
//*                      (in IEBUPDTE SYSIN format)                 *   FILE 133
//*                                                                 *   FILE 133
//*           ASM      - ASSEMBLER LANGUAGE SOURCE FOR SOME USEFUL  *   FILE 133
//*                      UTILITIES (now contains old assembler      *   FILE 133
//*                      source - possibly still useful for MVS     *   FILE 133
//*                      3.8.)                                      *   FILE 133
//*                                                                 *   FILE 133
//*                      New assembler source is now broken out     *   FILE 133
//*                      into individual members, together with     *   FILE 133
//*                      sample assembly JCL.                       *   FILE 133
//*                                                                 *   FILE 133
//*                 CPCMD    - ENABLES MVS USERS RUNNING UNDER VM   *   FILE 133
//*                            TO ISSUE CP COMMANDS AND GET THE     *   FILE 133
//*                            RESPONSES BACK AT THEIR TSO          *   FILE 133
//*                            TERMINAL.  CAN ALSO EXECUTED AS A    *   FILE 133
//*                            BATCH PROGRAM OR STARTED TASK.       *   FILE 133
//*                            LINK IT WITH AN ALIAS OF CP.  ON     *   FILE 133
//*                            TSO THEN ENTER CP Q DASD FOR         *   FILE 133
//*                            EXAMPLE, OR CP ATT 58A MVS.          *   FILE 133
//*                                                                 *   FILE 133
//*                 DASDSUB  - GET DASD DEVICE INFORMATION FROM     *   FILE 133
//*                            UCB. (USED BY SVTOC IN PLI.)         *   FILE 133
//*                                                                 *   FILE 133
//*                 DISASM3B - THE SVC TABLE FROM THE               *   FILE 133
//*                            DISASSEMBLER ON THE CBT TAPE.        *   FILE 133
//*                            MODIFIED FOR MVSXA AND COPIED INTO   *   FILE 133
//*                            SVCTAB.                              *   FILE 133
//*                            (Adjusted slightly by Sam Golob      *   FILE 133
//*                            to remove most of the user SVC's     *   FILE 133
//*                            and to add a few new IBM entries.)   *   FILE 133
//*                                                                 *   FILE 133
//*                 DSSLVL   - DISPLAY CURRENT DF/DSS PROGRAM       *   FILE 133
//*                            LEVEL.                               *   FILE 133
//*                                                                 *   FILE 133
//*                 JULSUB   - DATE CONVERSION SUBROUTINE.          *   FILE 133
//*                            (Adjusted slightly by Sam Golob.)    *   FILE 133
//*                                                                 *   FILE 133
//*                 LASTCLPA - COMMAND TO DISPLAY DATE AND TIME     *   FILE 133
//*                            OF LAST CLPA. A COMPANION PROGRAM    *   FILE 133
//*                            TO LASTIPL WHICH IS ON THE CBT       *   FILE 133
//*                            TAPE.                                *   FILE 133
//*                            (Fixed to create PUTLINE output      *   FILE 133
//*                             by S.Golob, Mar, 2012)              *   FILE 133
//*                            (Original version is LASTCLPO which  *   FILE 133
//*                             uses TPUT terminal output.)         *   FILE 133
//*                            (Fixed for z/OS 2.2 whose release    *   FILE 133
//*                             number '77A0' sorts lower than      *   FILE 133
//*                             z/OS 1.2, whose number is '7705'.   *   FILE 133
//*                             Used CVTOSLV3 to determine level,   *   FILE 133
//*                             instead of release number.)         *   FILE 133
//*                                                                 *   FILE 133
//*                 LNKLST   - DISPLAY NAMES OF LINKLST DATASETS    *   FILE 133
//*                            CURRENTLY IN USE.                    *   FILE 133
//*                                                                 *   FILE 133
//*                 LOGTIME  - TSO COMMAND TO DISPLAY LOGON TIME    *   FILE 133
//*                            AND DATE FOR THIS TSO SESSION.       *   FILE 133
//*                            (Taken from PSCB Logon Time field    *   FILE 133
//*                            and formatted like LISTCLPA display) *   FILE 133
//*                                                                 *   FILE 133
//*                 RACFDS   - DISPLAY DATA ABOUT THE RACF          *   FILE 133
//*                            DATASET(S) IN USE.                   *   FILE 133
//*                                                                 *   FILE 133
//*                 SMFDS    - DISPLAY DATA ABOUT CURRENT SMF       *   FILE 133
//*                            DATASET USAGE.                       *   FILE 133
//*                                                                 *   FILE 133
//*                 SVCTAB   - PROGRAM TO DISPLAY SVCTABLE.         *   FILE 133
//*                            (Enhanced by Sam Golob. Please see   *   FILE 133
//*                            notes in member SVCTAB#.)            *   FILE 133
//*                                                                 *   FILE 133
//*                 TODCN    - PROGRAM TO CONVERT TIMESTAMPS INTO   *   FILE 133
//*                            REAL DATES AND TIMES.                *   FILE 133
//*                                                                 *   FILE 133
//*                 VSAMNAME - CONVERT AND DISPLAY 'REAL' DATASET   *   FILE 133
//*                            NAMES ASSIGNED BY VSAM FOR PAGE,     *   FILE 133
//*                            MAN ETC.                             *   FILE 133
//*                                                                 *   FILE 133
//*           MACROS   - MACROS NECESSARY TO ASSEMBLE SOURCE IN     *   FILE 133
//*                      MEMBER ASM.  (Member contains old macros   *   FILE 133
//*                      to fit the source in the old ASM member.)  *   FILE 133
//*                                                                 *   FILE 133
//*                      (Macros are now broken out into indivi-    *   FILE 133
//*                      dual pds members, marked with id MACRO.)   *   FILE 133
//*                                                                 *   FILE 133
//*           SVTOC    - A PL/I UTILITY TO SORT IEHLIST LISTVTOC    *   FILE 133
//*                      OUTPUT INTO ADDRESS ORDER.                 *   FILE 133
//*                                                                 *   FILE 133
~~~~~~~~~~~~~~~~

