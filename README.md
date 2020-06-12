# utl-space-used-by-parent-folders-on-c-drive-without-subdirectory-for-file-space
Space used by parent folders on a drive without subdirectory for file space   
    Space used by parent folders on a drive without subdirectory for file space                                                             
                                                                                                                                            
    github                                                                                                                                  
    https://tinyurl.com/y82txf46                                                                                                            
    https://github.com/rogerjdeangelis/utl-space-used-by-parent-folders-on-c-drive-without-subdirectory-for-file-space                      
                                                                                                                                            
    macros                                                                                                                                  
    https://tinyurl.com/y9nfugth                                                                                                            
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                              
                                                                                                                                            
    Ther may be very large hiidden files like                                                                                               
    pagefile.sys                                                                                                                            
    swapfile.sys                                                                                                                            
    hiberfil.sas                                                                                                                            
                                                                                                                                            
    To see thess turn on in folder preferences                                                                                              
                                                                                                                                            
    Show hidden files and                                                                                                                   
    show hidden system files                                                                                                                
                                                                                                                                            
    This solution uses a drop down to powershell.                                                                                           
    Space used by files that are not in a floder is not reported.                                                                           
    For example pagefile.sys.                                                                                                               
                                                                                                                                            
    *_                   _                                                                                                                  
    (_)_ __  _ __  _   _| |_                                                                                                                
    | | '_ \| '_ \| | | | __|                                                                                                               
    | | | | | |_) | |_| | |_                                                                                                                
    |_|_| |_| .__/ \__,_|\__|                                                                                                               
            |_|                                                                                                                             
    ;                                                                                                                                       
                                                                                                                                            
    filename pipes pipe 'DIR c:\';                                                                                                          
    data have;                                                                                                                              
       retain dirlst;                                                                                                                       
       length dirlst $8192;                                                                                                                 
       infile pipes end=eod;                                                                                                                
       input @'>' folder & $255.;                                                                                                           
       put folder;                                                                                                                          
       * eod does not work with 2 processing;                                                                                               
       call symputx(cats("dirlst",_n_),folder);                                                                                             
       call symputx("dirlstn",_n_);                                                                                                         
    run;quit;                                                                                                                               
                                                                                                                                            
    Folders on C drive                                                                                                                      
                                                                                                                                            
     c:\                                                                                                                                    
       boot                                                                                                                                 
       cfg                                                                                                                                  
       Dell                                                                                                                                 
       etc                                                                                                                                  
       keys                                                                                                                                 
       oto                                                                                                                                  
       PerfLogs                                                                                                                             
       Program Files                                                                                                                        
       Program Files (x86)                                                                                                                  
       Python27                                                                                                                             
       python38                                                                                                                             
       R362                                                                                                                                 
       temp                                                                                                                                 
       Users                                                                                                                                
       utl                                                                                                                                  
       ver                                                                                                                                  
       Windows                                                                                                                              
                                                                                                                                            
    *            _               _                                                                                                          
      ___  _   _| |_ _ __  _   _| |_                                                                                                        
     / _ \| | | | __| '_ \| | | | __|                                                                                                       
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                        
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                       
                    |_|                                                                                                                     
    ;                                                                                                                                       
                                                                                                                                            
    Up to 40 obs from WANT total obs=17                                                                                                     
                                                                                                                                            
    Obs    FOLDER                   SIZE_MB                                                                                                 
                                                                                                                                            
      1    boot                       0.00                                                                                                  
      2    cfg                        0.45                                                                                                  
      3    Dell                       0.00                                                                                                  
      4    etc                       12.30                                                                                                  
      5    keys                       1.34                                                                                                  
      6    oto                       25.52                                                                                                  
      7    PerfLogs                   0.00                                                                                                  
      8    Program Files          13408.79                                                                                                  
      9    Program Files (x86)     1623.82                                                                                                  
     10    Python27                  65.10                                                                                                  
     11    python38                 407.62                                                                                                  
     12    R362                     882.34                                                                                                  
     13    temp                       0.04                                                                                                  
     14    Users                   3501.71                                                                                                  
     15    utl                      141.76                                                                                                  
     16    ver                      432.27                                                                                                  
     17    Windows                17189.95                                                                                                  
                                 =========                                                                                                  
                                  37693.01                                                                                                  
    *                                                                                                                                       
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                      
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                                     
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                                     
    | .__/|_|  \___/ \___\___||___/___/                                                                                                     
    |_|                                                                                                                                     
    ;                                                                                                                                       
                                                                                                                                            
    %utlnopts;                                                                                                                              
    %symdel i mb / nowarn;                                                                                                                  
                                                                                                                                            
    %let mb=-1;                                                                                                                             
                                                                                                                                            
    %macro _want(dummy);                                                                                                                    
                                                                                                                                            
      %local i dir;                                                                                                                         
                                                                                                                                            
      proc datasets lib=work nolist;                                                                                                        
        delete want;                                                                                                                        
      run;quit;                                                                                                                             
                                                                                                                                            
      %do i=1 %to &dirlstn;                                                                                                                 
                                                                                                                                            
         %let dir =&&dirlst&i;                                                                                                              
                                                                                                                                            
         * drop down to powershell - returns space in mb bia SAS macro variable;                                                            
         %utl_submit_ps64(resolve('                                                                                                         
           -f ((gci –force "c:\&dir" -Recurse -ErrorAction SilentlyContinue| measure Length -s).sum / 1MB | clip);'),return=mb);            
                                                                                                                                            
         data _want1;                                                                                                                       
             length folder $255 size 8.;                                                                                                    
             folder="&dir";                                                                                                                 
             size_mb=symgetn('mb');                                                                                                         
         run;quit;                                                                                                                          
                                                                                                                                            
         proc append data=_want1 base=want;                                                                                                 
         run;quit;                                                                                                                          
                                                                                                                                            
      %end;                                                                                                                                 
                                                                                                                                            
    %mend _want;                                                                                                                            
                                                                                                                                            
    %_want;                                                                                                                                 
                                                                                                                                            
                                                                                                                                            
                                                                                                                                            
                                                                                                                                            
