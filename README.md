# Intel® X<sup>e</sup>SS Plugin for Unity* Engine

## Introduction
This plugin integrates Intel® Xe Super Sampling (X<sup>e</sup>SS) into the Unity Engine.
* The plugin now supports the HDRP/SRP render pipeline.
* Supported graphics API: DX12/Vulkan/DX11.

Intel® X<sup>e</sup>SS enables innovative framerate boosting technology supported by Intel® Arc™ graphics cards and other GPU vendors. Using AI deep-learning for upscaling, X<sup>e</sup>SS offers higher framerates without degrading image quality.
For more information, visit: [Intel® X<sup>e</sup>SS GitHub](https://github.com/intel/xess)

If you encounter any integration issues, feel free to use the [Intel® XeSS Inspector](https://github.com/GameTechDev/XeSSInspector). This tool is specifically designed to simplify the validation and debugging of XeSS integration within applications.

## Components
* `com.intel.xess` - XeSS main C# package for Unity for XeSS SDK
* `UnityXeSSPlugin` - XeSS native plugin source code for Unity
* `com.unity.render-pipelines.high-definition@14.0.11` - Modified Unity HDRP rendering pipeline (14.0.11) code for Unity 2022 LTS
* `HDRP Samples` - Please check the "Release" section for the samples (with `vk.bat` to start with Vulkan, `dx12.bat` to start with DX12, and `dx11.bat` to start with DX11)

## How to Enable XeSS in HDRP Samples
### Integrating `com.intel.xess` into HDRP Unity Sample
* Use this HDRP template to create the HDRP project in Unity 2022 LTS version.

![Create Sample](Docs/create_sample.png?raw=true "Create Sample")

* When the project is loaded, close the project and move the `\Library\PackageCache\com.unity.render-pipelines.high-definition@14.0.11` folder to the `\Packages` folder with the XeSS package as shown below. This will allow you to modify the HDRP pipeline with your code.

![Package Folder](Docs/package_folder.png?raw=true "Package Folder")

* Replace the `com.unity.render-pipelines.high-definition@14.0.11` with the modified one in the repository to enable XeSS for HDRP.

* Ensure the core plugin `Packages\com.intel.xess\RunTime\Bin\XeSSRenderingPlugin.dll` is loaded on startup.

![Plugin Load on Startup](Docs/loadonstartup.png?raw=true "Plugin Load on Startup")

* Enable dynamic resolution support in the pipeline settings.

![Enable Dynamic Resolution](Docs/enable_dynamic.png?raw=true "Enable Dynamic Resolution")

### Check XeSS in the HDCamera Settings
* XeSS supported only

![XeSS Only](Docs/xess_only.png?raw=true "XeSS Only")

* DLSS & XeSS supported, with DLSS having higher priority

![DLSS and XeSS](Docs/dlss_xess.png?raw=true "DLSS and XeSS")

**_Attention: Both DLSS & XeSS require dynamic resolution to be enabled!_**

## Integrating `com.intel.xess` into Your Own HDRP/SRP Details
* An XeSS context corresponds to an HDCamera in Unity HDRP.
* The main XeSS pass integration is located in `com.unity.render-pipelines.high-definition@14.0.11\Runtime\RenderPipeline\RenderPass\XeSSPass.cs`.
* Use `com.intel.xess` to integrate your own XeSS in SRP and use `XeSSPass.cs` as a reference.

## Known Unity Plugin Issue
* Unity has a DX12 plugin fix in version 2022.3.39f1. Ensure your Unity engine version is greater than or equal to 2022.3.39f1.

![Unity Issue](Docs/unity_issue.png?raw=true "Unity Issue")

## For Unity 6
* You can directly use the `com.intel.xess` module in Unity6. For the HDRP render pipeline, there are two patches available in the 'Unity6Patch' folder: one for 'com.unity.render-pipelines.core' and another for 'com.unity.render-pipelines.high-definition'.