file(GLOB TEST_FILES *.png *.wxmx *.wxm *.mac)

if(WIN32)
    install(FILES ${TEST_FILES} DESTINATION wxMaxima/data)
else()
    install(FILES ${TEST_FILES} DESTINATION share/wxMaxima)
endif()
file(COPY ${TEST_FILES} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

# Test if maxima is working
add_test(NAME runMaxima WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND echo "quit();" | maxima)
set_tests_properties(runMaxima PROPERTIES TIMEOUT 60)

# Test if maxima is able to communicate with a backend
add_test(NAME runMaxima-over-network WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND echo 'quit() ;' | nc -l 40000 & sleep 10 ; maxima -s 40000)
set_tests_properties(runMaxima-over-network PROPERTIES TIMEOUT 60)

add_test(NAME wxmaxima_batch_textcell WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/textcells.wxm)
add_test(NAME wxmaxima_batch_foreign_characters WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/foreign-characters.wxm)
add_test(NAME wxmaxima_version_string WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --version)
set_tests_properties(wxmaxima_version_string PROPERTIES  PASS_REGULAR_EXPRESSION "wxMaxima ${VERSION}.*")
add_test(NAME wxmaxima_version_returncode WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --version)
add_test(NAME wxmaxima_help WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --help)

add_test(NAME all_celltypes WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_all_celltypes.wxm)
set_tests_properties(all_celltypes PROPERTIES TIMEOUT 60)

add_test(NAME simpleInput WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_simpleInput.wxm)
set_tests_properties(simpleInput PROPERTIES TIMEOUT 60)

add_test(NAME rememberingAnswers WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_rememberingAnswers.wxm)
set_tests_properties(rememberingAnswers PROPERTIES TIMEOUT 60)

add_test(NAME absCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_absCells.wxm)
set_tests_properties(absCells PROPERTIES TIMEOUT 60)

add_test(NAME diffCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_diffCells.wxm)
set_tests_properties(diffCells PROPERTIES TIMEOUT 60)

add_test(NAME atCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_atCells.wxm)
set_tests_properties(atCells PROPERTIES TIMEOUT 60)

add_test(NAME conjugateCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_conjugateCells.wxm)
set_tests_properties(conjugateCells PROPERTIES TIMEOUT 60)

add_test(NAME exptCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_exptCells.wxm)
set_tests_properties(exptCells PROPERTIES TIMEOUT 60)

add_test(NAME fracCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_fracCells.wxm)
set_tests_properties(fracCells PROPERTIES TIMEOUT 60)

add_test(NAME intCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_intCells.wxm)
set_tests_properties(intCells PROPERTIES TIMEOUT 60)

add_test(NAME functionCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_functionCells.wxm)
set_tests_properties(functionCells PROPERTIES TIMEOUT 60)

# Broken on Travis:
#add_test(NAME slideshowCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_slideshowCells.wxm)
#set_tests_properties(slideshowCells PROPERTIES TIMEOUT 60)

add_test(NAME imageCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_imageCells.wxm)
set_tests_properties(imageCells PROPERTIES TIMEOUT 60)

add_test(NAME limitCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_limitCells.wxm)
set_tests_properties(limitCells PROPERTIES TIMEOUT 60)

add_test(NAME matrixCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_matrixCells.wxm)
set_tests_properties(matrixCells PROPERTIES TIMEOUT 60)

add_test(NAME parenthesisCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_parenthesisCells.wxm)
set_tests_properties(parenthesisCells PROPERTIES TIMEOUT 60)

add_test(NAME sqrtCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_sqrtCells.wxm)
set_tests_properties(sqrtCells PROPERTIES TIMEOUT 60)

add_test(NAME subCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_subCells.wxm)
set_tests_properties(subCells PROPERTIES TIMEOUT 60)

add_test(NAME subsupCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_subsupCells.wxm)
set_tests_properties(subsupCells PROPERTIES TIMEOUT 60)

add_test(NAME sumCells WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_sumCells.wxm)
set_tests_properties(sumCells PROPERTIES TIMEOUT 60)

# Is mysteriously broken on travis.
# add_test(NAME printf_simple WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_printf_simple.wxm)
# set_tests_properties(printf_simple PROPERTIES TIMEOUT 60)
#
# add_test(NAME printf_equations WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_printf_equations.wxm)
# set_tests_properties(printf_equations PROPERTIES TIMEOUT 60)
#
# add_test(NAME printf_continuationLines WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_printf_continuationLines.wxm)
# set_tests_properties(printf_continuationLines PROPERTIES TIMEOUT 60)

add_test(NAME weirdLabels WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_weirdLabels.wxm)
set_tests_properties(weirdLabels PROPERTIES TIMEOUT 60)

add_test(NAME xmlQuote WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_xmlQuote.wxm)
set_tests_properties(xmlQuote PROPERTIES TIMEOUT 60)

add_test(NAME formerCrashes WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_formerCrashes.wxm)
set_tests_properties(formerCrashes PROPERTIES TIMEOUT 60)

add_test(NAME multiplication WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_multiplication.wxm)
set_tests_properties(multiplication PROPERTIES TIMEOUT 60)

add_test(NAME nonsenseConstructs WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_nonsenseConstructs.wxm)
set_tests_properties(nonsenseConstructs PROPERTIES TIMEOUT 60)

add_test(NAME lisp WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_lisp.wxm)
set_tests_properties(lisp PROPERTIES TIMEOUT 60)

add_test(NAME boxes WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_boxes.wxm)
set_tests_properties(boxes PROPERTIES TIMEOUT 60)

add_test(NAME unicode WORKING_DIRECTORY ${CMAKE_BINARY_DIR} COMMAND ./wxmaxima-local --batch test/testbench_automatic_unicode.wxm)
set_tests_properties(unicode PROPERTIES TIMEOUT 60)


