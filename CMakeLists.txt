cmake_minimum_required(VERSION 3.22)
project(XFormant VERSION 1.0.0)

add_subdirectory(JUCE)

juce_add_plugin(XFormant
        COMPANY_NAME "AlmondRyan"
        PLUGIN_MANUFACTURER_CODE "Alry"
        PLUGIN_CODE "XFrm"
        FORMATS VST3 AU Standalone
        PRODUCT_NAME "XFormant"

        IS_SYNTH FALSE
        NEEDS_MIDI_INPUT TRUE
        NEEDS_MIDI_OUTPUT FALSE
        IS_MIDI_EFFECT FALSE
        EDITOR_WANTS_KEYBOARD_FOCUS TRUE
        COPY_PLUGIN_AFTER_BUILD TRUE
)


target_sources(XFormant
    PRIVATE
        Source/PluginEditor.cpp
        Source/PluginProcessor.cpp)

target_compile_definitions(XFormant
    PUBLIC
        # JUCE_WEB_BROWSER and JUCE_USE_CURL would be on by default, but you might not need them.
        JUCE_WEB_BROWSER=0  # If you remove this, add `NEEDS_WEB_BROWSER TRUE` to the `juce_add_plugin` call
        JUCE_USE_CURL=0     # If you remove this, add `NEEDS_CURL TRUE` to the `juce_add_plugin` call
        JUCE_VST3_CAN_REPLACE_VST2=0)


target_link_libraries(XFormant
    PRIVATE
        juce::juce_audio_basics
        juce::juce_audio_devices
        juce::juce_audio_formats
        juce::juce_audio_plugin_client
        juce::juce_audio_processors
        juce::juce_audio_utils
        juce::juce_core
        juce::juce_data_structures
        juce::juce_dsp
        juce::juce_events
        juce::juce_graphics
        juce::juce_gui_basics
        juce::juce_gui_extra
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)
