CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

foreach(TARGET tok-embed segrnn-sup poisson-regression tag-bilstm embed-cl encdec xor xor-xent xor-batch xor-batch-lookup rnnlm rnnlm-aevb rnnlm-cfsm rnnlm-batch nlm textcat rnnlm2 rnnlm-mp read-write)
  ADD_EXECUTABLE(${TARGET} ${TARGET}.cc)
  target_link_libraries(${TARGET} cnn ${LIBS} rt pthread)
  if (WITH_CUDA_BACKEND)
    add_dependencies(${TARGET} cnncuda)
    target_link_libraries(${TARGET} cnncuda)
    CUDA_ADD_CUBLAS_TO_TARGET(${TARGET})
  endif (WITH_CUDA_BACKEND)
endforeach()

