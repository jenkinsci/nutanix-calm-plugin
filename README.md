# Nutanix Calm Plugin
Nutanix Calm Jenkins plugin allows you to launch Nutanix Calm blueprint, provision infrastructure, and services in a multi cloud environment and subsequently run actions/tasks on those applications.

#### License:
* All source code is licensed under the MIT license.

#### Supported Versions:
* Jenkins versions: 2.107.2 and later
* Nutanix Calm versions: 5.7.1 and later
* Google Chrome version:  69.0.3497.100 (Official Build) (64-bit)

#### Plugin Installation:
* Download the plugin file from this link [Nutanix Calm Jenkins Plugin](https://github.com/nutanix/Nutanix-Calm-Jenkins-Plugin/releases/download/v1.0/nutanix-calm.hpi).
* Navigate to Manage Jenkins→ Manage Plugins → Advanced.  Upload the plugin file.
  ![](Docs/screenshots/Upload_plugin.png)
* To verify that the Nutanix Calm plug-in is successfully installed, click Manage Jenkins→ Manage Plugins→ Installed search for Nutanix Calm plugin.
  ![](Docs/screenshots/Verify_plugin.png)

#### Plugin Configuration:
* To configure the plugin first Navigate to Manage Jenkins -> Configure System -> Nutanix Calm Plugin Configuration. Provide the Prism Central IP, Username and Password.
  ![](Docs/screenshots/Plugin_configuration.png)

#### Jenkins Freestyle job Setup:
* Click on New Item.Select Freestyle project. Enter an item name. Click OK.
  ![](Docs/screenshots/Click_on_newitem.png)
  ![](Docs/screenshots/Select_freestyle_project.png)
* Click on Add Build step. Select **Nutanix Calm Blueprint Launch**.
  ![](Docs/screenshots/Select_bp_launch_step.png)
* In the section
    * Select the Calm project.
    * Select the Blueprint to launch. Blueprint description is fetched and displayed.
    * Select the Application profile.
    * Modify the values for runtime variables available for that application profile.
    * Provide an application name. BUILD_ID is appended by default to the application name to uniquely identify it in Calm.
    * Select the option if you want Jenkins job to wait for blueprint launch to complete before proceeding to the next step.
      ![](Docs/screenshots/Enter_bp_launch_step.png)
* To invoke actions defined in the Calm blueprint/ application, click on Add Build Step. Select **Nutanix Calm Application Action Run**.
  ![](Docs/screenshots/Select_app_action_step.png)
* In the section
    * Select the application name.
    * Select the application actions available.
    * If necessary, modify the values for the runtime variables available.
      ![](Docs/screenshots/Enter_app_action_step.png)
    * Click on Apply and then Save.
    * Now we can click on **Build Now** to run these build steps and then we can check the console output for this build.
    * ![](Docs/screenshots/Build_Now_Freestyle_Project.png)

#### Jenkins Pipeline:
* Click on New Item. Select Pipeline. Enter an item name. Click OK.
  ![](Docs/screenshots/Click_on_newitem.png)
  ![](Docs/screenshots/Select_pipeline.png)
* Select pipeline script in Pipeline Definition section and to generate the pipeline syntax click on the Pipeline Syntax at the bottom.
  ![](Docs/screenshots/Select_Pipeline_Script.png)
* In the Pipeline Syntax window, select the General build Step in the Sample step dropdown.
  * Select Nutanix Calm Blueprint Launch in Build Step
* In the section
    * Select the Calm project.
    * Select the Blueprint to launch. Blueprint description is fetched and displayed.
    * Select the Application profile.
    * Modify the values for runtime variables available for that application profile.
    * Provide an application name. BUILD_ID is appended by default to the application name to uniquely identify it in Calm.
    * Select the option if you want Jenkins job to wait for blueprint launch to complete before proceeding to the next step.
    * Click on Generate Pipeline Script.
      ![](Docs/screenshots/Pipeline_bp_launch.png)
* Copy and paste the text in the box below into the pipeline script box in **{}** under node.
  ![](Docs/screenshots/Copy_bp_launch_script.png)
* Follow same steps to generate the pipeline syntax for **Nutanix Calm Application Action Run**.
  ![](Docs/screenshots/Pipeline_bp_launch.png)
* Copy and paste the text in the box below into the pipeline script box in **{}** under node.
  ![](Docs/screenshots/Copy_App_Action_Script.png)
* Click on Apply and then Save.
* Now we can click on **Build Now** to run these build steps and then we can check the console output for this build.
* ![](Docs/screenshots/Build_Now_Pipeline.png)

* We can also use Pipeline script from SCM in Pipeline Definition section
  ![](Docs/screenshots/Pipeline_scm.png)

* Please find the below mentioned pipeline/jenkinsfile syntax for our reference for **Nutanix Calm Blueprint Launch** and **Nutanix Calm Application Action Run** build steps.
    * Nutanix Calm Blueprint Launch
    > step([$class: 'BlueprintLaunch', appProfileName: 'Enter_Application_Profile_name', applicationName: 'Enter_application_name_${BUILD_ID}', blueprintDescription: 'Enter_blueprint_description>', blueprintName: 'Enter_blueprint_name>', projectName: 'Enter_project_name', runtimeVariables: '''{
          <"key": "value">
      }''', waitForSuccessFulLaunch: Enter_true_or_false])

    * Nutanix Calm Application Action Run
    > step([$class: 'RunApplicationAction', actionName: 'Enter_Action_name', applicationName: 'Enter_Application_name_${BUILD_ID}', runtimeVariables: '''{
          <"key": "value">
      }'''])

    * NOTE: We need to put the required build steps pipeline script in **node{}** for pipeline/jenkinsfile invocation.

