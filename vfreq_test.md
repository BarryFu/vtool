    *** Settings ***

    Library     OperatingSystem

    Library     diff

    Resource    ../../common_keyword/vfreq_keyword.robot

    Suite Setup  Directory Should Exist  ../../temple 


    *** Variables ***

    ${files_dir}=  ../../temple/vfreq_test_temple

    ${outcar}=  ${files_dir}/OUTCAR

    ${g09log}=  ${files_dir}/H2Ofreq

    ${g09log_temple}=  ${files_dir}/H2Ofreq_temple

    ${g09log_diff_result}=   vfreq_diff

    ${helper_temple}=  ${files_dir}/vfreq_helper_temple
    
    ${hint_temple}=  ${files_dir}/vfreq_hint_temple


*** Keywords ***

Generate g09freq From OUTCAR
    Run vfreq  ${outcar}  ${g09log}

Check g09freq
    diff_context  ${g09log}  ${g09log_temple}  ${g09log_diff_result}
    ${rc}  ${result}=  Run and Return RC and Output  cat ${g09log_diff_result}
    Should Be Empty  ${result}

Check g09freq Without Output File
    ${rc}  ${result}=  Run and Return RC and Output  vfreq -i ${outcar}
    ${rc}  ${result1}=  Run and Return RC and Output  cat ${g09log_temple}
    Should Be Equal  ${result}  ${result1}

Generate vfreq Helper  
    Run vfreq 

Check vfreq Helper
    ${rc}  ${result}=  Run and Return RC and Output  vfreq -h
    ${rc}  ${result1}=  Run and Return RC and Output  cat  ${helper_temple}
    Should Be Equal  ${result}  ${result1}

Check vfreq Hint
    ${rc}  ${result}=  Run and Return RC and Output  vfreq
    ${rc}  ${result1}=  Run and Return RC and Output  cat  ${helper_temple}
    Should Be Equal  ${result}  ${result1}



*** Test Cases ***
Convert OUTCAR To g09log
    [Setup]  File Should Exist  ${g09log_temple}
    Generate g09freq From OUTCAR
    Check g09freq
    Check g09freq Without Output File 
    [Teardown]  Remove Files  ${g09log_diff_result}  ${g09log}

#OBCheck vfreq Helper
#   Test Setup OUTCAR To g09log helper
#    Run vfreq helper
#     Check vfreq Helper

#Check vfreq Hint
#    Test Setup OUTCAR To g09log hint
#    Run vfreq hint
#    Check vfreq Hint
