# The name of the package:
atlas_subdir (bTagger)

#atlas_depends_on_subdirs( PUBLIC
#                          InnerDetector/InDetRecTools/InDetTrackSelectionTool
#                          Tools/PathResolver
#                          )


# Add the shared library:
atlas_add_library (bTaggerLib
  bTagger/*.h Root/*.cxx
  PUBLIC_HEADERS bTagger
  LINK_LIBRARIES JetUncertaintiesLib PathResolver ParticleJetToolsLib JetCalibToolsLib InDetTrackSelectionToolLib MuonAnalysisInterfacesLib TrigDecisionToolLib TriggerMatchingToolLib TrigConfInterfaces AnaAlgorithmLib EventLoopAlgs EventLoop xAODHIEvent xAODEgamma xAODMuon xAODJet xAODEventInfo AsgAnalysisInterfaces)

# Add the dictionary:
atlas_add_dictionary (bTaggerDict
  bTagger/bTaggerDict.h
  bTagger/selection.xml
  LINK_LIBRARIES bTaggerLib)

if (NOT XAOD_STANDALONE)
  # Add a component library for AthAnalysis only:
  atlas_add_component (bTagger
    src/components/*.cxx
    LINK_LIBRARIES bTaggerLib)
endif ()

# Install files from the package:
atlas_install_joboptions( share/*.py )
atlas_install_data( data/* )
