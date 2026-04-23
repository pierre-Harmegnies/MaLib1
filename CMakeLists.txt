cmake_minimum_required(VERSION 3.10)
project(MaLib1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

# Création de la bibliothèque partagée (.so)
add_library(MaLib1 SHARED src/lib1.cpp)

# Gestion des dossiers d'include (Crucial pour l'export)
target_include_directories(MaLib1 PUBLIC 
    # Quand on compile MaLib1, on cherche dans le dossier include local
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    # Quand MaLib1 est installée, les clients chercheront dans 'include' (relatif au prefix)
    $<INSTALL_INTERFACE:include>
)

# Configuration de l'installation de la cible
install(TARGETS MaLib1 
    EXPORT MaLib1Targets     # On prépare un groupe d'export nommé MaLib1Targets
    DESTINATION lib          # Où copier le fichier .so
    INCLUDES DESTINATION include # Où les clients doivent chercher les headers
)

# Installation du header public
install(FILES include/lib1.h DESTINATION include)

# Génération du fichier MaLib1Config.cmake (pour find_package)
install(EXPORT MaLib1Targets
    FILE MaLib1Config.cmake  # Le nom du fichier que find_package cherchera
    DESTINATION lib/cmake/MaLib1 # Emplacement standard pour les fichiers config
)
