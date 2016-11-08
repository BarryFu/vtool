*** Keywords ***
Test Setup POSCAR To vscan
    File Should Exist  ${poscar}

#Test Setup POSCAR To vscan Hint
#    File Should Exist  ${vscan_temple}

#Test Setup POSCAR To vscan Helper
#    File Should Exist  ${vscan_temple}

Run vscan linear 
    [Arguments]  ${input}=${None}   
    ${rc}  ${result}=  Run and Return RC and Output  vscan -i ${input} -r 92 -m 93 -g 92,93 -n 4 -d 0.1 
    Should Be Equal  ${0}  ${rc}

Run vscan angle
    [Arguments]  ${input}=${None}
    ${rc}  ${result}=  Run and Return RC and Output  vscan -i ${input} -r 74,92 -m 93 -g 74,92,93 -n 5 -d 2
    Should Be Equal  ${0}  ${rc}

Run vscan dihedral
    [Arguments]  ${input}=${None}
    ${rc}  ${result}=  Run and Return RC and Output  vscan -i ${input} -r 73,74,92 -m 93 -g 74,92,93 -n 5 -d 2
    Should Be Equal  ${0}  ${rc}

run vscan hint
    ${rc}  ${result}=  Run and Return RC and Output  vscan
    Should Be Equal  ${1}  ${rc}

Run vscan helper
    ${rc}  ${result}=  Run and Return RC and Output  vscan -h
    Should Be Equal  ${0}  ${rc}


