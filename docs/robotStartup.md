



1. **Calibration Step:**
   * When the `step` is in the 'calibration' phase and the `calibrationDialog` is not active, it displays an image (`image_openCalibration.png`) and four tips with corresponding numbers and messages.
   * A warning message is displayed at the bottom.
5. **Device Connection Step:**
   * When the `step` is in the 'connect' phase and there's no active calibration dialog:
     * It shows an image (`image_deviceConnect.png`) and displays initial account information.
     * A connection tip is shown.
6. **Program Startup Step:**
   * In the 'startup' phase and without an active calibration dialog:
     * It shows different images and messages based on whether the system is still initializing or has successfully initialized.
     * A loading message is displayed during initialization.
7. **Calibration Dialog:**
   * The `calibrationDialog` section shows a dialog with images illustrating calibration poses and corresponding tips. It can be closed with a close button.
8. **Operate Area:**
   * Buttons in this section allow users to navigate between different steps (`calibration`, `connect`, `startup`) based on the system's current state.
   * The buttons have different appearances based on the step and connectivity status.
   * A "Finish" button is displayed with an icon for completed steps.
9. **Prompt Box:**
   * A prompt box is displayed based on the `promptVisible` variable, allowing users to confirm or cancel certain actions.

### logic:

1. **State Management:**
   * The `stateOn` method enables debug state and listens for messages from the robot. When the system is fully initialized (`all_init`), it sets `isReady` to true.
2. **Step Navigation:**
   * The `changeStep` method is responsible for transitioning between steps based on certain conditions.
3. **Program Startup:**
   * The `getStartup` method sends a request to start the program. After a delay, it enables debug state to monitor initialization progress.
4. **Shutdown:**
   * The `shutDown` method is triggered when the user decides to shut down the program. It disables debug state, closes the control server, and resets the system state.### Overall Functionality:

# Robot Startup Interface Technical Documentation

## Introduction

The Robot Startup Interface Component is a Vue.js component designed to facilitate the startup process for a robot. This document provides an overview of the component's structure, functionality, and usage.

## 1. Template Section

### 1.1 Header

The header section utilizes the `rtc-header` component, displaying the current state of the robot startup in the `headState` section.

### 1.2 Startup Steps

The template dynamically renders different sections based on the `step` variable, representing Calibration, Device Connection, and Program Startup steps. Each step includes specific content, such as images, tips, and information.

### 1.3 Calibration Dialog

If the `calibrationDialog` variable is `true`, a modal dialog appears displaying calibration images and tips with step numbers.

### 1.4 Operate Area

This section contains buttons for different steps in the startup process. Button appearance and behavior depend on the `step` and `connected` status, providing actions like starting calibration, connecting devices, starting the program, and shutting down.

### 1.5 Prompt Box

A modal dialog (`prompt-box`) appears if the `promptVisible` variable is `true`, displaying confirmation buttons for actions like shutting down the program.

## 2. Script Section

### 2.1 Imports

The component imports necessary components (`rtc-header`, `prompt-box`) and mixins (`Heartbeat`). Additionally, the `mapState` function from Vuex is used.

### 2.2 Data and Methods

The component defines data variables (`step`, `calibrationDialog`, `isReady`, `promptVisible`) and methods for actions like enabling/disabling debug states, changing steps, starting exploration, and handling shutdown.

### 2.3 Lifecycle Hooks

Utilizes lifecycle hooks (`created`, `mounted`, `destroyed`) for component initialization and cleanup.

### 2.4 Computed Properties

Uses Vuex's `mapState` to map `connected` and `robot` state variables.

This technical document provides a comprehensive understanding of the Robot Startup Interface Component, outlining its structure, functionality, and styling considerations. Developers can refer to this document for implementation details and customization options.
