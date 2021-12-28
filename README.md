# AS400
Basic Math operations using AS400 DSPF &amp; RPGLE


# RPGLE PROGRAM SEU
H                                                      
FCALC1     CF   E             WORKSTN                  
 *                                                     
 /FREE                                                 
  DoW *IN03=*OFF;                                      
   EXFMT CALCR;                                        
   EMSG=*BLANKS;                                       
   SELECT;                                             
   WHEN OPC='+';                                       
    OPT=NUM1+NUM2;                                     
   WHEN OPC='-';                                       
    OPT=NUM1-NUM2;                                     
   WHEN OPC='*';                                       
    MONITOR;                                           
     OPT=NUM1*NUM2;                                    
    ON-ERROR;             
      EMSG='RESULT OUT OF RANGE';                 
 OPT=0;                                      
ENDMON;                                      
WHEN OPC='/'  ;                              
 MONITOR;                                    
   OPT=NUM1/NUM2;                            
 ON-ERROR;                                   
  EMSG='CANNOT DIVIDE BY ZERO';              
  OPT=0;                 
   ENDMON;                                          
 WHEN *IN05=*ON;                                   
  NUM1=0;                                          
  NUM2=0;                                          
  OPT=0;                                           
  *IN05=*OFF;                                      
 OTHER;                                            
  EMSG='ENTER VALID OP CODE & NUMBERS';            
  OPT=0;                                           
 ENDSL;                                         
 ENDDO;                                          
 *INLR=*ON;                                       
/END-FREE     


# DDS code using SDA
 A*%%TS  SD  20211228  110737  PAVANS      REL-V7R4M0  5770-WDS 
 A*%%EC                                                         
 A                                      DSPSIZ(24 80 *DS3)      
 A          R CALCR                                             
 A*%%TS  SD  20211228  110737  PAVANS      REL-V7R4M0  5770-WDS 
 A                                      CA03(03 'EXIT')         
 A                                      CA05(05 'REFRESH')      
 A                                  1 33'AS400 CALCULATOR'      
 A                                      DSPATR(UL)              
 A                                      COLOR(BLU)              
 A                                  1 62USER                    
 A                                  2 62DATE                    
 A                                      EDTCDE(Y)               
 A                                  3 62TIME                    
 A                                  5 12'ENTER THE 1ST NUMBER:' 
 A                                  7 12'ENTER THE OP CODE   :' 
 A                                  9 12'ENTER THE 2ND NUMBER:'  
 A                                 11 12'FINAL RESULT        :'  
 A                                 23 12'F3=EXIT'                
 A                                 23 30'F5=REFRESH'             
 A            EMSG          30A  O 16 13DSPATR(HI)               
 A                                      COLOR(RED)               
 A            NUM1           3S 0I  5 34                         
 A            OPC            1A  I  7 34                         
 
 
 A            NUM2           3S 0I  9 34                         
