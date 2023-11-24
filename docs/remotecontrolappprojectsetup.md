# Build Your Own Remote Control App

## Prerequisites

Ensure that you have the following tools installed before proceeding:

* [Hbuilder](https://www.dcloud.io/hbuilderx.html)

## Build Instructions

1. **Clone or Download Source Code:**

   * Clone the RoCS App repository or download the source code archive:
     * [Download Zip](https://github.com/FFTAI/rocs_app/archive/refs/tags/v1.1.zip)
     * [Download Tarball](https://github.com/FFTAI/rocs_app/archive/refs/tags/v1.1.tar.gz)
2. **Project Packaging:**

   * Open a terminal and navigate to the project root directory.
   * Execute the following command to package the project:

     ```bash
     npm run build
     ```

3. **Open Hbuilder and Create a New Project:**

   * Open Hbuilder and create a new project.
   * Choose project type as "5+App."
   * Set the project name and location as desired.
4. **Project Setup:**

   * After project creation, retain the `unpackage` folder and `manifest.json`.
   * Replace all files in the new project (except `unpackage` and `manifest.json`) with the contents of the `dist` folder generated during the build.
5. **Configure `manifest.json`:**

   * Open `manifest.json` and configure it according to your requirements.
6. **Cloud Build:**

   * In Hbuilder, navigate to `Build`  -> `Mobile App - Cloud Packaging`.
   * Wait for the APK generation process to complete.
7. **Final Steps:**

   * Once the build is finished, you will find the generated APK in the specified output directory.

!> This guide assumes familiarity with Hbuilder and the basics of 5+App development.

!> Customize the `manifest.json` file to meet your specific application requirements.

!> The provided source code serves as a reference project, and developers are encouraged to modify it according to your needs.
