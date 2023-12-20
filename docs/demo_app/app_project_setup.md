# Build Your Own Remote Control App

For advanced users and developers, building a customized APK based on the Control App source code allows for tailored functionalities and enhancements. Follow the procedures below to build your own remote control app.

# Development Setup

### Dependencies

To ensure a smooth development process, the following libraries and frameworks are essential:

1. **Vue.js** : The core framework. Ensure you have the latest stable version.
2. **Vuex** : For state management within Vue.js.
3. **Vue Router** : For managing navigation within the application.
4. **Axios** : For making HTTP requests to the API.
5. **Node.js** : The runtime environment for executing JavaScript code server-side.
6. **Webpack** : For module bundling.
7. **Babel** : For JavaScript compilation.
8. **ESLint** : For code linting and maintaining coding standards.
9. **Jest** : For unit testing.
10. **Sass** : For advanced styling capabilities.

### Environment Setup

Setting up your development environment involves the following steps:

1. **Install Node.js and npm** :

* Download and install Node.js from [nodejs.org](https://nodejs.org/).
* npm (Node Package Manager) comes bundled with Node.js.
* Verify installation by running `node -v` and `npm -v` in your terminal.

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

#### Running Locally

To run the application locally:

1. **Local Development Server** :

* Execute `npm run serve` in the terminal. This command starts a local development server.
* The application will be hosted at `http://localhost:8080` by default. You can access it using a web browser.

1. **Live Reloading** :

* The local server comes with hot-reloading. Any changes made to the source code will automatically refresh the application in the browser.

1. **Accessing Application Features** :

* Test different features like robot control and system settings as they would function in the production environment.

1. **Running Unit Tests** :

* Execute `npm run test` to run unit tests. This ensures your local changes haven't broken existing functionalities.

1. **Linting Code** :

* Run `npm run lint` to identify and fix linting issues, ensuring code consistency.

Following these steps will set up a robust development environment, enabling you to efficiently develop, test, and debug the application.

## **APP Architecture Overview**

The app's user interface is constructed using Vue.js components. These components encapsulate specific features, such as navigation, user prompts, and control interfaces. The interaction between components is managed through Vue Router, facilitating a smooth transition between different views.

Vuex plays a pivotal role in maintaining the state of the application. The central store, organized into modules, holds critical information like the robot's connection status, control type, and other relevant data. Mutations and actions in Vuex ensure controlled and predictable state changes, providing a foundation for the app's dynamic behavior.

```powershell
├─components
│      promptBox.vue
│      rDialog.vue
│      rtcHeader.vue
│      rtcLeftControl.vue
│
├─i18n
│  │  i18n.js
│  │
│  └─locale
│          en.json
│          tw.json
│          zh-CN.json
│
├─mixin
│      Heartbeat.js
│
├─router
│      index.js
│
├─store
│      index.js
│
└─views
    ├─connect
    │      Connect.vue
    │
    ├─controller
    │      Controller.vue
    │
    ├─development
    │      Development.vue
    │
    ├─loading
    │      Loading.vue
    │
    ├─login
    │      Login.vue
    │
    ├─robotStartup
    │      RobotStartup.vue
    │
    ├─setting
    │      Setting.vue
    │
    └─startUp
            StartUp.vue
```

* **components**: Contains Vue components that can be reused across application.

  * **promptBox.vue**: Vue component for displaying prompt boxes.
  * **rDialog.vue**: Vue component for displaying dialog boxes.
  * **rtcHeader.vue**: Vue component for the header of the application.
  * **rtcLeftControl.vue**: Vue component for the left control panel.
* **i18n**: Internationalization (i18n) configuration and translation files.

  * **i18n.js**: Configuration for i18n.
  * **locale**: Translation files for different languages.
* **mixin**: Contains mixins used in the application.

  * **Heartbeat.js**: A mixin for handling heartbeat functionality.
* **router** : Configuration for the Vue Router.
* **store** : Configuration for Vuex (state management).
* **views** : Contains Vue components for different views/pages of the application.
* **connect** : View for connecting to a device.

  * **Connect.vue** : The main Vue component for connecting to a device.
* **controller** : View for controlling the device.

  * **Controller.vue** : The main Vue component for controlling the device.
* **development** : Development-related view.

  * **Development.vue** : The main Vue component for development-related tasks.
* **loading** : View for loading screens.

  * **Loading.vue** : The main Vue component for loading screens.
* **login** : View for the login screen.

  * **Login.vue** : The main Vue component for the login screen.
* **robotStartup** : View for robot startup tasks.

  * **RobotStartup.vue** : The main Vue component for robot startup tasks.
* **setting** : View for application settings.

  * **Setting.vue** : The main Vue component for application settings.
* **startUp** : View for application startup tasks.

  * **StartUp.vue** : The main Vue component for application startup tasks.

### API Integration

1. **Robot Interaction** :

* Endpoint: `/robot/sdk_ctrl/start`
* Purpose: To start the robot and initiate its functions.
* Method: GET
* Data Flow: Triggered in `RobotStartup.vue`, this API call starts the robot. The response is monitored to update the UI accordingly.

1. **System Settings** :

* Endpoint: `/robot/control_svr_status`
* Purpose: Checks the status of the robot server.
* Method: GET
* Usage: In `Login.vue`, this endpoint determines if the robot server is active before proceeding.

1. **Shut Down Robot** :

* Endpoint: `/robot/control_svr_close`
* Purpose: To shut down the robot server.
* Method: GET
* Implementation: Used in `RobotStartup.vue` to turn off the robot.

### Data Flow

1. **Initialization** :

* The application starts with `Startup.vue`, displaying the initial logo and then navigating to `Login.vue`.
* `Login.vue` checks the robot server status before allowing users to proceed.

1. **Robot Operation Flow** :

* `Controller.vue` takes user inputs for robot control. These inputs are sent to the robot through API calls.
* Responses from the robot are received and processed to update the UI or handle errors.

1. **Settings and Information** :

* `Setting.vue` fetches and displays system information and settings.
* Users can update settings, and changes are sent to the server via API calls.

### Error Handling and Debugging

* API errors are handled gracefully, with user-friendly messages displayed.
* `RobotStartup.vue` includes provisions for logging and debugging, essential for troubleshooting issues during robot operation.
