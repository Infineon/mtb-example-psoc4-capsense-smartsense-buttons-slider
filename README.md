# PSoC&trade; 4: CAPSENSE&trade; SmartSense buttons slider

This code example demonstrates how to tune self-capacitance (CSD)-based buttons and slider widgets with SmartSense in PSoC&trade; 4 devices using the CAPSENSE&trade; tuner.

This document provides a high-level overview of the CSD widgets tuning flow and details on how to use the CAPSENSE&trade; tuner to monitor the CAPSENSE&trade; raw data and fine-tune the CSD buttons and slider for optimum performance.


[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-capsense-smartsense-buttons-slider)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzc1MzIiLCJTcGVjIE51bWJlciI6IjAwMi0zNzUzMiIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IENBUFNFTlNFJnRyYWRlOyBTbWFydFNlbnNlIGJ1dHRvbnMgc2xpZGVyIiwicmlkIjoicmFqYW5uYWdhdXRhIiwiRG9jIHZlcnNpb24iOiIxLjAuMCIsIkRvYyBMYW5ndWFnZSI6IkVuZ2xpc2giLCJEb2MgRGl2aXNpb24iOiJNQ0QiLCJEb2MgQlUiOiJJQ1ciLCJEb2MgRmFtaWx5IjoiUFNPQyJ9)

## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) v3.1 or later (tested with v3.1)
- Board support package (BSP) minimum required version: 3.0.0
- Programming language: C
- Associated parts: [PSoC&trade; 4000S and PSoC&trade; 4100S Plus](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-4-32-bit-arm-cortex-m0-mcu/)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; Embedded Compiler v11.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; Compiler v6.16 (`ARM`)
- IAR C/C++ Compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 4100S Plus prototyping kit](https://www.infineon.com/CY8CKIT-149) (`CY8CKIT-149`) - Default value of `TARGET`
- [PSoC&trade; 4000S CAPSENSE&trade; prototyping kit](https://www.infineon.com/CY8CKIT-145-40XX) (`CY8CKIT-145-40XX`)

## Hardware setup

This example uses the board's default configuration. See the kit user guide to ensure that the board is configured correctly.

**Note:** PSoC&trade; 4 kits ship with KitProg2 installed. The ModusToolbox&trade; software requires KitProg3. Before using this code example, make sure that the board is upgraded to KitProg3. The tool and instructions are available in the [Firmware-loader](https://github.com/Infineon/Firmware-loader) GitHub repository. If you do not upgrade, you will see an error like "unable to find CMSIS-DAP device" or "KitProg firmware is out of date".

## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The "project-creator-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

<br />

The following example clones the "[CAPSENSE&trade; SmartSense buttons slider](https://github.com/Infineon/mtb-example-psoc4-capsense-smartsense-buttons-slider)" application with the desired name "CapsenseSmartsenseButtonsSlider" configured for the [*CY8CKIT-149*](https://www.infineon.com/CY8CKIT-149) BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-149 --app-id mtb-example-psoc4-capsense-smartsense-buttons-slider --user-app-name CapsenseSmartsenseButtonsSlider --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) to choose the BSP for the supported kit. You can invoke the Library Manager GUI tool from the terminal using `make library-manager` command or use the Library Manager CLI tool "library-manager-cli" to change the BSP.

The "library-manager-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--add-bsp-name` | Name of the BSP that should be added to the application | Required
`--set-active-bsp` | Name of the BSP that should be as active BSP for the application | Required
`--add-bsp-version`| Specify the version of the BSP that should be added to the application if you do not wish to use the latest from manifest | Optional
`--add-bsp-location`| Specify the location of the BSP (local/shared) if you prefer to add the BSP in a shared path | Optional

<br />

Following example adds the [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149) BSP to the already created application and makes it the active BSP for the app:

   ```
   library-manager-cli --project "C:/mtb_projects/CapsenseSmartsenseButtonsSlider" --add-bsp-name CY8CKIT-149 --add-bsp-version "latest-v3.X" --add-bsp-location "local"

   library-manager-cli --project "C:/mtb_projects/CapsenseSmartsenseButtonsSlider" --set-active-bsp APP_CY8CKIT-149
   ```

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool:**

   1. Launch Project Creator from the Windows Start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.

   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.

   3. In the **Select Application** screen, select the appropriate IDE from the **Target IDE** drop-down menu.

   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.

<br />

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>


## Operation

The following steps explain the tuning procedure. Because the project already has the necessary settings by default, you can skip this procedure and go to [Testing the basic operation](#testing-the-basic-operation) to verify the operation. To understand the tuning process and follow the steps for this kit or your own board, see [Tuning procedure](#tuning-procedure).

**Note:** For more details on SmartSense, see the "SmartSense full auto-tune" section in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951).

### Tuning procedure

SmartSense is a CAPSENSE&trade; tuning method that automatically sets sensing parameters for optimal performance based on user-specified Finger capacitance (pF) values and continuously compensates for system, manufacturing, and environmental changes.
In SmartSense Full Auto-tune mode, the only parameter that needs to be tuned by the user is the Finger capacitance (pF) parameter. The Finger capacitance (pF) parameter indicates the minimum value of Finger capacitance (pF) that should be detected as a valid touch by the CAPSENSE&trade; widget.

**Note:** Even for SmartSense auto-tuning, the CAPSENSE&trade; allows manual configuration of some general parameters like enabling and disabling of compensation IDAC, filters, shield such as liquid-tolerance related parameters and modulator clock. These can be left at their default values for most cases or configured based on the requirements.


####  Tuning button widgets

**Figure 1. CSD button widgets tuning flow**

![](images/button-tuning-flow-chart.png)

Do the following to tune the slider:

<details><summary><b>Stage 1: Select the highest Finger capacitance (pF) value</b></summary>

1. Connect to CAPSENSE&trade; tuner by following the steps in the [Testing the basic operation](#testing-the-basic-operation) section.

2. Select the **Button0**, **Button1**, and **Button2** checkboxes and select **Synchronized** under **Read mode** and then navigate to **Graph View** as shown in **Figure 2**.

   The **Graph View** shows the raw counts and baseline for **Button0**, **Button1**, and **Button2** in the **Sensor data** window. Ensure that the **Raw counts** and **Baseline** checkboxes are selected to view the sensor data.

   **Figure 2. CAPSENSE&trade; tuner graph view**

   ![](images/button_graph_view.png)
   
3. In the **Widget hardware parameters** section, select **Finger capacitance (pF)** value as 1 (highest Finger capacitance (pF)) and click on **Apply to device** symbol to apply the changes to the device as shown in **Figure 3**.
   
   **Figure 3. CAPSENSE&trade; Widget hardware parameters**

   ![](images/button_max_finger_capacitance.png)
   
   **Note:** The valid range of **Finger capacitance (pF)** is 0.1 to 1.

</details>

<details><summary><b>Stage 2: Coarse tuning</b></summary>

1. Measure the signal and calculate the SNR.

   1. Switch to the **SNR Measurement** tab for measuring the SNR and to verify that the SNR is above 5:1, select **Button0** and **Button0_Sns0** sensor, and then click **Acquire Noise** as shown in **Figure 4**.

      **Figure 4. CAPSENSE&trade; tuner - SNR measurement: acquire noise**
   
      ![](images/button_acquire_noise_signal.png)

   2. Once the noise is acquired, place the finger at a position on the button and then click **Acquire Signal**. Ensure that the finger remains on the button as long as the signal acquisition is in progress. Observe that the SNR is above 5:1.

      The calculated SNR on this button is displayed, as shown in **Figure 5**. Based on your end system design, test the signal with a finger that matches the size of your normal use case. Typically, finger size targets are ~8 to 9 mm. Consider testing with smaller sizes that should be rejected by the system to ensure that they do not reach the finger threshold.

      **Figure 5. CAPSENSE&trade; tuner - SNR measurement: acquire signal**

      ![](images/button_acquire_signal.png)
     
2. Is SNR > 5:1 & Does sensor status change to 1 on touch?
 
     1. Switch to the **Graph View** tab to verify the status change. Place the finger at a position on the button and see the status graph. 
      
        Observe there is no change in the status signal for Finger capacitance (pF) value 1 as shown in **Figure 6**.

        **Figure 6. CAPSENSE&trade; tuner - Status signal**

        ![](images/button_status_signal.png) 
      
     2. For Finger capacitance (pF) value 1, SNR > 5:1 but status signal is zero on touch.
     
3. Choose the next lower value of Finger capacitance (pF).

    1. If the Finger capacitance (pF) value does not satify the both conditions (SNR > 5:1 & sensor status change to 1 on touch), choose the next lower value of Finger capacitance (pF).
    
    2. Repeat step 1 and step 2 in coarse tuning process and verify both conditions.
    
    3. Repeat the step 3 until both conditions are satisfied.
    
       For this case, both conditions are satisfied for the Finger capacitance (pF) value 0.50, as shown in **Figure 7** and **Figure 8**.
    
        **Figure 7. CAPSENSE&trade; tuner - Status signal**

        ![](images/button_status_signal_1.png) 
      
       **Figure 8. CAPSENSE&trade; tuner - SNR measurement**

        ![](images/button_snr_measurement.png)
        
    **Note:** Coarse-tuning satisfies the requirements of most designs, but fine-tuning allows you to choose the most efficient CAPSENSE&trade; parameters (that is, minimum sensor scan time) using the SmartSense.

</details>

<details><summary><b>Stage 3: Fine tuning</b></summary>

1. Choose the next higher value of Finger capacitance (pF).

   The next higher value of Finger capacitance (pF) is 0.60. Change the Finger capacitance (pF) value to 0.50 to 0.60 and click on **Apply to device**, as shown in **Figure 9**.
   
      **Figure 9. CAPSENSE&trade; Apply to device button**

      ![](images/apply-to-device.png)
   
2. Measure the signal and calculate the SNR.

   1. Follow the same procedure explained in coarse tuning step1 to measure the SNR.
   

3. Is SNR > 5:1 & Does sensor status change to 1 on touch?

   1. Follow the same procedure explained in coarse tuning step2 and verify the conditions.

4. Choose the Finger capacitance (pF) value.
   
   1. If the Finger capacitance (pF) value does not satisfy the conditions in step3, skip to step5.
   
   2. If the Finger capacitance (pF) value satisfy the conditions in step3, choose that Finger capacitance (pF) value.


5. Decrease the Finger capacitance (pF) to a value in between the current and the next lower available value.

   The next lowest value between 0.60 and 0.50 is 0.59. Change the Finger capacitance (pF) value to 0.59 and click on **Apply to device** button as shown in **Figure 9**.
   
6. Repeat the step2, step3 and step4 for optimal Finger capacitance (pF) value.

   After following the steps the optimal value of Finger capacitance (pF) for **Button0** is 0.53.
   
Repeat the entire tuning process for **Button1** and **Button2**.

</details>

**Note:** The following tuning steps are done on [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149). Follow the same tuning procedure for [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX) kit.

The optimal Finger capacitance (pF) values after tuning is:

 Widget  |  [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149) | [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX) |
 :------- | :------------    | :-----------  |
 Button0 | 0.53 | 1 |
 Button1 | 0.35 | 0.79 |
 Button2 | 0.26 | 0.57 |

#### Tuning slider widgets


**Figure 10. CSD slider widget tuning flow**  

![](images/slider-tuning-flow-chart.png)

**Note:**

*To review slider design, see the **Slider design** section in the **Design considerations** chapter in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951).

** To do manual tuning, see the **Manual tuning** section in the **CAPSENSE&trade; performance tuning** chapter in the [PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951).
   
Do the following to tune the slider: 

<details><summary><b>Stage 1: Set the Finger capacitance (pF) value to the maximum allowed</b></summary>

1. Connect to CAPSENSE&trade; tuner by following the steps in  [Testing the basic operation](#testing-the-basic-operation) section.

2. Select the **LinearSlider0** check box and select **Synchronized** under **Read mode**, and then navigate to **Graph View** as shown in **Figure 11**.

   The **Graph View** shows the raw counts and baseline for **LinearSlider0** in the **Sensor data** window. Ensure that the **Raw counts** and **Baseline** checkboxes are selected to view the sensor data.

   **Figure 11. CAPSENSE&trade; tuner graph view**

   ![](images/slider_graph_view.png)
   
3. In the **Widget hardware parameters** section select **Finger capacitance (pF)** value as 1 (highest Finger capacitance (pF)) and Click on **Apply to device** symbol to apply the changes to the device as shown in **Figure 12**.
   
   **Figure 12. CAPSENSE&trade; Widget hardware parameters**

   ![](images/slider_max_finger_capacitance.png)
   
   **Note:** The valid range of **Finger capacitance (pF)** is 0.1 to 1.

</details>   

<details><summary><b>Stage 2: Slide finger over the slider and monitor the difference count i.e., Sensor Signal</b></summary>

   Observe the **Sensor Signal** in **Graph View** section (see **Figure 13**) while sliding the finger. There is no change in the Sensor Signal for Finger capacitance (pF) value 1.
   
   **Figure 13. CAPSENSE&trade; Sensor Signal**

   ![](images/slider_sensor_signal.png)

</details>

<details><summary><b>Stage 3: At any finger position, do atleast two slider segments provide difference count (Sensor Signal > 0)?</b></summary>

At any finger position, if atleast two slider segments provides Sensor Signal > 0 , **Skip** to stage 4. If not, continue the process.

1. Is Finger capacitance (pF) >= minimum allowed Finger capacitance (pF) value?

   The minimum allowed Finger capacitance (pF) value is 0.1. Check the given Finger capacitance (pF) value is >= 0.1.
   
   If the value is less than 0.1, **End the tuning process**.
   
   A hardware change may be required. Review slider design* or use manual tuning**.

   If the value is not less than 0.1, continue the process.
   
   
2. Decrease Finger capacitance (pF) value by one unit.

   1. Decrease the **Finger capacitance (pF)** value by one unit in **Widget hardware parameters** section and click on **Apply to device** symbol to apply the changes to the device as shown in **Figure 14**.
   
      **Figure 14. CAPSENSE&trade; Graph view**

      ![](images/slider_finger_capacitance_1.png)
      
   2. Repeat the process from **Stage 2**.

</details>

<details><summary><b>Stage 4: At any finger position, does at least one slider segment provide an SNR > 5:1 and sensor signal > 50?</b></summary>

1. Measure the signal, calculate the SNR and verify SNR > 5:1.

   1. Switch to the **SNR Measurement** tab for measuring the SNR and to verify that the SNR is above 5:1, select **LinearSlider0**, **LinearSlider0_Sns0** sensor, and then click **Acquire Noise** as shown in **Figure 15**.

      **Figure 15. CAPSENSE&trade; tuner - SNR measurement: acquire noise**
   
      ![](images/slider_acquire_noise_signal.png)

   2. Once the noise is acquired, place the finger at a position on the selected Linear Slider sensor and then click **Acquire Signal**. Ensure that the finger remains on the Linear Slider sensor as long as the signal acquisition is in progress and observe the SNR.

      The calculated SNR on this LinearSlider0 is displayed, as shown in **Figure 16**. Based on your end system design, test the signal with a finger that matches the size of your normal use case. Typically, finger size targets are ~8 to 9 mm. Consider testing with smaller sizes that should be rejected by the system to ensure that they do not reach the finger threshold.
 
      **Figure 16. CAPSENSE&trade; tuner - SNR measurement: acquire signal**

      ![](images/slider_acquire_signal.png)
     
2.  Verify sensor signal > 50?

     1. Switch to the **Graph View** tab to verify the sensor signal. Place the finger at a position on the LinearSlider sensor and see the status graph. 
      
        Observe there is no change in the sensor signal for Finger capacitance (pF) value 0.9, as shown in **Figure 17**.

        **Figure 17. CAPSENSE&trade; tuner - Status signal**

        ![](images/slider_sensor_signal_1.png) 

3. Repeat step1 and step2 for LinearSlider0_Sns1, LinearSlider0_Sns2, LinearSlider0_Sns3, LinearSlider0_Sns4 and LinearSlider0_Sns5.

   **Note:** For [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX) kit, only five slider segments present (LinearSlider0_Sns0, LinearSlider0_Sns1, LinearSlider0_Sns2, LinearSlider0_Sns3 and LinearSlider0_Sns4).
   
4. If at any finger position, at least one slider segment provides an SNR > 5:1 and sensor signal > 50 choose that Finger capacitance (pF).

   By following the above process at Finger capacitance (pF) value 0.2 both conditions satisfy as shown in the **Figure 18** and **Figure 19**
   
    **Figure 18. CAPSENSE&trade; tuner - LinearSlider Sensor signal**

    ![](images/slider_sensor_signal_2.png)
     
    **Figure 19. CAPSENSE&trade; tuner - LinearSlider SNR measurement**

    ![](images/slider_snr_measurement.png)
  
5. If both conditions did not satisfy, **Skip** to Stage 3. Repeat the process from there.

</details>

**Note:** The following tuning steps are done on [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149). Follow the same tuning procedure for [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX) kit.
   
The optimal Finger capacitance (pF) values after tuning is:

 Widget | [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149) | [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX) |
:--------|:-------------|:------------------|
 LinearSlider0 | 0.2 | 0.7 |


## Testing the basic operation

1. Connect the board to your PC using the provided micro USB cable through the KitProg3 USB connector.

2. Program the board.

   - **Using Eclipse IDE for ModusToolbox&trade; software:**

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3)**.

   - **Using CLI:**

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain is specified in the application's Makefile but you can override this value manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```

      After programming, the application starts automatically. 

3. Launch the CAPSENSE&trade; tuner to monitor the CAPSENSE&trade; data and for CAPSENSE&trade; parameter tuning, and SNR measurement.
 
   See the [CAPSENSE&trade; Tuner guide](https://www.infineon.com/ModusToolboxCapSenseTuner) for step-by-step instructions on how to launch and configure the CAPSENSE&trade; Tuner in the ModusToolbox&trade; software.

4. Go to **Tools** > **Tuner Communication Setup** and set the parameters as shown in **Figure 20**. Click **OK**.

   **Figure 20. Tuner Communication Setup**

   ![](images/tuner-configuration-setup.png)

5. Click **Connect**.

   **Figure 21. CAPSENSE&trade; tuner window**

   ![](images/connect-symbol.png)

6. Click **Start**.

   **Figure 22. CAPSENSE&trade; tuner start**

   ![](images/start-symbol.png)

   The **Widget/Sensor Parameters** tab gets updated with the parameters configured in the **CAPSENSE&trade; Configurator** window.

   **Figure 23. CAPSENSE&trade; tuner window**

   ![](images/capsense-tuner-window.png)

7. Observe the **Widget/Sensor Parameters** section in the CAPSENSE&trade; Tuner window.

8. Touch the CAPSENSE&trade; buttons and slide your finger over the CAPSENSE&trade; linear slider. Observe the status signal change to 0 to 1 on touch.

## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

## Design and implementation

The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; software user guide for more details on selecting the middleware). See [AN85951 – PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details on CAPSENSE&trade; features and usage.

The design has a CSD-based, three buttons, CAPSENSE&trade; slider, and EZI2C peripheral. The EZI2C slave peripheral is used to monitor the sensor data of buttons, slider and slider touch position information on a PC using the CAPSENSE&trade; tuner available in the Eclipse IDE for ModusToolbox&trade; via I2C communication.  

The code scans the widgets using the CSD sensing method and sends the CAPSENSE&trade; raw data over an I2C interface to the CAPSENSE&trade; tuner GUI tool on a PC using the on-board KitProg USB-I2C bridge.

### Resources and settings

#### [CY8CKIT-149](https://www.infineon.com/CY8CKIT-149)
1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. Launch the CAPSENSE&trade; configurator tool.
   
   The CAPSENSE&trade; configurator tool can be launched in Eclipse IDE for ModusToolbox&trade; from the 'CSD peripheral' setting in the device configurator or in stand-alone mode directly from the Project Explorer.

   See the [ModusToolbox&trade; CAPSENSE&trade; configurator tool guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in the ModusToolbox&trade; software. 

3. In the **Basic** tab, a single slider **LinearSlider0** and three buttons (**Button0**, **Button1** and **Button2**) are configured as a **CSD (Self-cap)**, and the CSD tuning mode is configured as **SmartSense (Full Auto-Tune)**. 

   **Figure 24. CAPSENSE&trade; configurator - Basic tab**  

   ![](images/basic-tab-149-kit.png)

4. Do the following in the **General** sub-tab under the **Advanced** tab:

   **Figure 25. CAPSENSE&trade; configurator - General sub-tab in Advanced Tab** 
   
   ![](images/advanced-general-tab-149-kit.png)

5. Go to the **CSD Settings** tab and make the following changes:
   
   - Select **Enable compensation IDAC**.

      **Figure 26. CAPSENSE&trade; configurator - CSD settings sub-tab in Advanced Tab** 
      
      ![](images/advanced-csd-settings-149-kit.png)

6. Go to the **Widget Details** tab. Observe that all the parameters are set by SmartSense.


   **Figure 27. CAPSENSE&trade; configurator - Widget Details in Advanced Tab** 
      
   ![](images/advanced-widget-details-149-kit.png)

7. Go to the **Pins** tab. Make the pin connections as shown in **Figure 28**.

     **Figure 28. CAPSENSE&trade; configurator - Pins Tab** 
      
      ![](images/pins-tab-149-kit.png)

8. Click **Save** to apply the settings.

#### [CY8CKIT-145-40XX](https://www.infineon.com/CY8CKIT-145-40XX)
1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. Launch the CAPSENSE&trade; configurator tool.
   
   The CAPSENSE&trade; configurator tool can be launched in Eclipse IDE for ModusToolbox&trade; from the 'CSD peripheral' setting in the device configurator or in stand-alone mode directly from the Project Explorer.

   See the [ModusToolbox&trade; CAPSENSE&trade; configurator tool guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in the ModusToolbox&trade; software. 

3. In the **Basic** tab, a single slider **LinearSlider0** and three buttons (**Button0**, **Button1** and **Button2**) are configured as a **CSD (Self-cap)**, and the CSD tuning mode is configured as **SmartSense (Full Auto-Tune)**. 

   **Figure 29. CAPSENSE&trade; configurator - Basic tab**  

   ![](images/basic-tab-145-kit.png)

4. Do the following in the **General** sub-tab under the **Advanced** tab:

   **Figure 30. CAPSENSE&trade; configurator - General sub-tab in Advanced Tab** 
   
   ![](images/advanced-general-tab-145-kit.png)

5. Go to the **CSD Settings** tab and make the following changes:
   
   - Select **Enable compensation IDAC**.

      **Figure 31. CAPSENSE&trade; configurator - CSD settings sub-tab in Advanced Tab** 
      
      ![](images/advanced-csd-settings-145-kit.png)

6. Go to the **Widget Details** tab. Observe that all the parameters are set by SmartSense.


   **Figure 32. CAPSENSE&trade; configurator - Widget Details in Advanced Tab** 
      
   ![](images/advanced-widget-details-145-kit.png)

7. Go to the **Pins** tab. Make the pin connections as shown in **Figure 33**.

     **Figure 33. CAPSENSE&trade; configurator - Pins Tab** 
      
      ![](images/pins-tab-145-kit.png)

8. Click **Save** to apply the settings.

**Table 1. Application resources**

 **Figure 34. Device configurator - EZI2C Pepipheral** 
      
 ![](images/ezi2c-configuration.png)

| Resource  |  Alias/object     |    Purpose     |
| :------- | :------------    | :------------ |
| SCB (I2C) (PDL) | CYBSP_EZI2C | EZI2C slave driver to communicate with the CAPSENSE&trade; tuner |
| CAPSENSE&trade; | CYBSP_CapSense | CAPSENSE&trade; driver to interact with the CSD hardware and interface CAPSENSE&trade; sensors |

### Firmware flow

**Figure 35. Firmware flowchart**

 ![](images/firmware-flow.png)

<br>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSoC&trade; 4
Code examples  | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub <br> [Using PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/software/code-examples/psoc-3-4-5-code-examples-for-psoc-creator/)
Device documentation | [PSoC&trade; 4 datasheets](https://www.infineon.com/cms/en/search.html#!view=downloads&term=psoc4&doc_group=Data%20Sheet) <br>[PSoC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!view=downloads&term=psoc4&doc_group=Additional%20Technical%20Information)
Development kits | Select your kits from the [Evaluation Board Finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) page.
Libraries on GitHub | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSoC&trade; 4 peripheral driver library (PDL)<br> [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Middleware on GitHub | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents <br>
Tools  | [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices. <br /> [PSoC&trade; Creator](https://www.infineon.com/cms/en/design-support/tools/sdk/psoc-software/psoc-creator/) – IDE for PSoC&trade; and FM0+ MCU development

<br />


## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE237532* - *PSoC&trade; 4: CAPSENSE&trade; SmartSense buttons slider*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example


<br />

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2023. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br />
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br />
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit www.infineon.com. Other names and brands may be claimed as property of their respective owners.
