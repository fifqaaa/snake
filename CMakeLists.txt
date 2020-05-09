cmake_minimum_required(VERSION 3.15)
project(snake)

set(CMAKE_CXX_STANDARD 14)


add_compile_options(-Wall -Wextra)

# ustawienia SFML-a dla Linuksa/MacOS i Windows - proszę zostawić obie konfiguracje,
# CMake automatycznie użyje właściwej
if (UNIX)
    # proszę nie modyfkować pierwszego wpisu, można dopisać kolejne katalogi
    # pierwszy wpis powinien poprawnie skonfigurować SFML-a dla wszystkich
    # Debianopodobnych dystrybucji
    set ( CMAKE_MODULES_PATH "/usr/share/SFML/cmake/Modules" ${CMAKE_MODULE_PATH})

    # czy ktoś używa MacOS ? Co tam trzeba wpisać ?

endif(UNIX)

if (WIN32)
    # próbujemy linkować statycznie (nie trzeba kopiować plików dll do katalogu projektu)
    set( SFML_STATIC_LIBRARIES TRUE )

    # można zmienić katalog na właściwy
    set ( SFML_DIR "C:/cpp/SFML-2.5.1/lib/cmake/SFML")
endif(WIN32)


# to polecenie się wywali, jeśli CMake nie znajdzie SFML-a w jednym ze wskazanych
# wcześniej katalogów - nie ma potrzeby robienia potem if-a dla target_link_libraries
find_package(SFML 2 REQUIRED graphics audio )


add_executable(snake main.cpp Game.cpp Game.h begin_window.cpp begin_window.h)

target_link_libraries(snake sfml-graphics sfml-audio)

# ABSOLUTNIE I W ŻADNYM WYPADKU nie dodawać wpisu include_directories(${SFML_PATH}/include/SFML/) !!!
# po pierwsze - nie jest potrzebny, po drugie - "dzięki" takim wpisom utrudniacie mi życie
# W kodzie w dyrektywach #include należy obowiązkowo używać konwencji #include <SFML/...>
