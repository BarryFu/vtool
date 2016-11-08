##*** Keywords ***


Test Setup OUTCAR To g09log

    File Should Exist  ${g09log_temple}


Test Setup OUTCAR To g09log Hint

    File Should Exist  ${g09log_temple}


Test Setup OUTCAR To g09log Helper

    File Should Exist  ${g09log_temple}


Run vfreq

    [Arguments]  ${input}=${None}  ${output}=${None} 

    ${cmd}=  Set Variable If

    ...  "${output}" == "${None}"  vfreq -i ${input}

    ...  vfreq -i ${input} -o ${output}

    ${rc}  ${result}=  Run and Return RC and Output  ${cmd}

    Should Be Equal  ${0}  ${rc}


Run vfreq hint

    ${rc}  ${result}=  Run and Return RC and Output  vfreq

    Should Be Equal  ${1}  ${rc}


Run vfreq helper

    ${rc}  ${result}=  Run and Return RC and Output  vfreq -h

    Should Be Equal  ${0}  ${rc}


