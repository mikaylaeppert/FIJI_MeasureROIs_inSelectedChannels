# MeasureROIs_inSelectedChannels

A simple [Fiji/ImageJ](https://imagej.net/software/fiji/) macro script to **measure mean intensity and area for ROIs across multiple channels**. This script loops through all ROIs in the ROI Manager and performs measurements on two specified image channels (channels 1 and 2).

## 📋 Requirements

- Fiji / ImageJ
- Open ROI Manager with ROIs added manually
- Set measurements in Fiji to:
  - Area
  - Mean gray value

## 🧠 Purpose

This macro is intended for fluorescence microscopy images where:
- ROIs (e.g., LacO foci) are manually selected
- Measurements are needed for both the focus and a corresponding nuclear background
- Two image channels need to be quantified per ROI

## 🧪 How It Works

1. Retrieves image dimensions and ROI count.
2. Iterates through each ROI in the ROI Manager.
3. For each ROI:
   - Sets the image to **Channel 1** and runs `Measure`
   - Sets the image to **Channel 2** and runs `Measure`
4. Updates and displays the results table.

## ▶️ Usage

1. Load your multi-channel image stack in Fiji.
2. Add ROIs to the ROI Manager:
   - Draw ROI around Lac focus
   - Press **T** to add
   - Move ROI to nuclear background
   - Press **T** again
3. Ensure measurements are set via:
   - `Analyze > Set Measurements…` → check **Area** and **Mean gray value**
4. Run the macro script.

## 📜 Macro Script

```javascript
// MeasureROIs_inSelectedChannels
// This ImageJ macro will run the "measure" command on Fiji on all ROIs in the ROI manager.
// Before running macro, set measurements to Area and Mean gray value and open ROI manager and
// then add ROIs to manager: Draw ROI around Lac focus (t) - move ROI to nuclear background (t)

// Image dimensions
getDimensions(width, height, channels, slices, frames);

// Number of ROIs
nRois = roiManager("count");

// Measure 2 channels for each ROI
for (i = 0; i < nRois; i++) {
    roiManager("select", i);

    // Measure 1st channel
    Stack.setChannel(1);
    run("Measure");

    // Measure 2nd channel
    Stack.setChannel(2);
    run("Measure");
}

// Show results
updateResults();
