cmake_minimum_required(VERSION 3.8)
project(main)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS "-fopenmp -fext-numeric-literals")
set(CMAKE_CXX_FLAGS_DEBUG "-Og -g3")
set(CMAKE_CXX_FLAGS_RELEASE "-Os -ftree-vectorize -s -g")

set(SOURCES
        main.cpp
        Exceptions.cpp
        Exceptions.h
        analysis/Analyser_mainLoop.cpp
        analysis/Analyser.cpp
        analysis/Analyser.h
        analysis/parts/formants.cpp
        analysis/parts/lpc.cpp
        analysis/parts/pitch.cpp
        analysis/parts/resample.cpp
        audio/AudioCapture.cpp
        audio/AudioCapture_callbacks.cpp
        audio/AudioCapture.h
        audio/RingBuffer.cpp
        audio/RingBuffer.h
        gui/AnalyserWindow.cpp
        gui/AnalyserWindow.h
        gui/SDLUtils.cpp
        gui/SDLUtils.h
        gui/Spectrogram.cpp
        gui/Spectrogram.h
        lib/Formant/Formant.cpp
        lib/Formant/Formant.h
        lib/LPC/Frame/LPC_Frame.cpp
        lib/LPC/Frame/LPC_Frame.h
        lib/LPC/Frame/LPC_Frame_auto.cpp
        lib/LPC/Frame/LPC_Frame_burg.cpp
        lib/LPC/Frame/LPC_Frame_covar.cpp
        lib/LPC/Frame/LPC_Frame_huber.cpp
        lib/LPC/LPC.cpp
        lib/LPC/LPC.h
        lib/LPC/LPC_filter.cpp
        lib/LPC/LPC_huber.cpp
        lib/LPC/LPC_huber.h
        lib/LPC/LPC_huber_stat.cpp
        lib/Math/Bairstow.cpp
        lib/Math/Bairstow.h
        lib/Math/Polynomial.cpp
        lib/Math/Polynomial.h
        lib/Math/Viterbi.cpp
        lib/Math/Viterbi.h
        lib/Pitch/McLeod/autocorrelation.cpp
        lib/Pitch/McLeod/parabolic_interpolation.cpp
        lib/Pitch/McLeod/peak_picking.cpp
        lib/Pitch/McLeod/MPM.h
        lib/Pitch/Pitch_AMDF.cpp
        lib/Pitch/Pitch_MPM.cpp
        lib/Pitch/Pitch.h
        lib/Signal/Filter.cpp
        lib/Signal/Filter.h
        lib/Signal/Resample.cpp
        lib/Signal/Resample.h
        lib/Signal/Window.cpp
        lib/Signal/Window.h
        lib/FFT/FFT.cpp
        lib/FFT/FFT.h
        lib/MFCC/MFCC.cpp
        lib/MFCC/MFCC.h
        analysis/parts/preemph.cpp
        lib/Formant/DF/features.cpp
        lib/Formant/DF/features.h)

find_package(Eigen3 3.3 REQUIRED NO_MODULE)
find_package(SDL2 REQUIRED)
find_package(SDL2_ttf REQUIRED)
find_package(SDL2_gfx REQUIRED)
find_package(PortAudio REQUIRED)
find_package(FFTW REQUIRED DOUBLE_LIB)

set(CMAKE_FIND_ROOT_PATH "${TORCH_INSTALL_DIR}")
find_package(Torch REQUIRED)

include_directories(
        ${PROJECT_SOURCE_DIR}/libs
        ${SDL2_INCLUDE_DIR}
        ${SDL2_TTF_INCLUDE_DIR}
        ${SDL2_GFX_INCLUDE_DIRS}
        ${EIGEN_INCLUDE_DIR}
        ${PORTAUDIO_INCLUDE_DIRS}
        ${FFTW_INCLUDE_DIRS}
        ${TORCH_INCLUDE_DIRS}
)

add_executable(speech_analysis ${SOURCES})

target_link_libraries(speech_analysis
        ${SDL2_LIBRARY}
        ${SDL2_TTF_LIBRARIES}
        ${SDL2_GFX_LIBRARIES}
        ${SDL2_LIBRARY}
        Eigen3::Eigen
        ${PORTAUDIO_LIBRARIES}
        ${FFTW_LIBRARIES}
        ${TORCH_LIBRARY}
)