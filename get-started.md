---
title: Build with PocketPose
layout: products
description: Get started with PocketPose and build your own pose estimation applications.
permalink: "/get-started/"
---

## Build with PocketPose

You can use PocketPose to build your own pose estimation applications. Select your preferences to get the right usage command.

<div class="container model-selector">

  <!-- Your OS -->
  <div class="row">
    <div class="selector-header">Your OS</div>
    <div class="options-grid" id="osOptions">
      <div class="option" data-value="Linux">Linux</div>
      <div class="option" data-value="Mac">Mac</div>
      <div class="option" data-value="Windows">Windows</div>
      <div class="option" data-value="Android">Android</div>
      <div class="option" data-value="Web">Web</div>
    </div>
  </div>

  <!-- Language -->
  <div class="row">
    <div class="selector-header">Language</div>
    <div class="options-grid" id="languageOptions">
      <div class="option" data-value="Python">Python</div>
      <div class="option" data-value="JavaScript">JavaScript</div>
      <div class="option" data-value="Kotlin">Kotlin</div>
    </div>
  </div>

  <!-- Model Type -->
  <div class="row">
    <div class="selector-header">Person Detector</div>
    <div class="options-grid" id="modelTypeOptions">
      <div class="option" data-value="RTMDet">RTMDet</div>
      <div class="option" data-value="YOLOX">YOLOX</div>
    </div>
  </div>

  <!-- Framework -->
  <div class="row">
    <div class="selector-header">Detection Quality</div>
    <div class="options-grid" id="frameworkOptions">
      <div class="option" data-value="Fast">Fast</div>
      <div class="option" data-value="Balanced">Balanced</div>
      <div class="option" data-value="High Accuracy">High Accuracy</div>
    </div>
  </div>

  <!-- Keypoints Format -->
  <div class="row">
    <div class="selector-header">Keypoints Format</div>
    <div class="options-grid" id="keypointsOptions">
      <div class="option" data-value="Body">Body</div>
      <div class="option" data-value="BodyWithFeet">Body + Feet</div>
      <div class="option" data-value="Face">Face</div>
      <div class="option" data-value="Hands">Hands</div>
      <div class="option" data-value="Wholebody">Wholebody</div>
    </div>
  </div>

  <!-- Compute Platform -->
  <div class="row">
    <div class="selector-header">Compute Platform</div>
    <div class="options-grid" id="computePlatformOptions">
      <div class="option" data-value="CPU">CPU</div>
      <div class="option" data-value="CUDA">CUDA</div>
      <div class="option" data-value="Metal">Metal</div>
    </div>
  </div>

  <!-- Generated Command -->
  <div class="row">
    <div class="selector-header">Run this Command:</div>
    <div class="options-grid">
      <div class="option install-command" id="generatedCommand">Select options to generate command.</div>
    </div>
  </div>
</div>

This command will automatically run the best model for your selected preferences. For researchers and the curious, see a complete list of supported models, their benchmarks, and how to run them [here](/models/).

## Learn More

Explore our comprehensive documentation to master PocketPose and create advanced pose estimation applications.

<div class="row">
  {% for service in site.products %}
  <div class="col-12 col-md-4 mb-3">
    <div class="service service-summary">
      <div class="service-content">
        <h3 class="service-title">
          <a href="{{ service.url | relative_url }}">{{ service.title }}</a>
        </h3>
        <p>{{ service.content | markdownify | strip_html | truncate: 100 }}</p>
      </div>
    </div>
  </div>
  {% endfor %}
</div>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const optionsGroups = {
      os: document.getElementById("osOptions"),
      language: document.getElementById("languageOptions"),
      modelType: document.getElementById("modelTypeOptions"),
      framework: document.getElementById("frameworkOptions"),
      keypoints: document.getElementById("keypointsOptions"),
      computePlatform: document.getElementById("computePlatformOptions"),
    };

    const selectedValues = {
      os: "",
      language: "",
      modelType: "",
      framework: "",
      keypoints: "",
      computePlatform: "",
    };

    function updateCommand() {
      const { modelType, framework, keypoints, computePlatform } = selectedValues;
      if (modelType && framework && keypoints && computePlatform) {
        document.getElementById("generatedCommand").innerText =
          `# Install PocketPose\npip install pocketpose\n\n# Run Image Inference\npocketpose-cli -m process_image\n  --det_model "${modelType}"\n  --det_quality "${framework}"\n  --pose_model "${keypoints}"\n  --device "${computePlatform}"`;
      } else {
        document.getElementById("generatedCommand").innerText = "Select options to generate command.";
      }
    }

    function setupSelection(group, key) {
      group.addEventListener("click", function (event) {
        if (event.target.classList.contains("option")) {
          [...group.children].forEach(option => option.classList.remove("selected"));
          event.target.classList.add("selected");
          selectedValues[key] = event.target.dataset.value;
          updateCommand();
        }
      });
    }

    setupSelection(optionsGroups.os, "os");
    setupSelection(optionsGroups.language, "language");
    setupSelection(optionsGroups.modelType, "modelType");
    setupSelection(optionsGroups.framework, "framework");
    setupSelection(optionsGroups.keypoints, "keypoints");
    setupSelection(optionsGroups.computePlatform, "computePlatform");

    // Select default options
    const defaultOptions = {
      os: "Linux",
      language: "Python",
      modelType: "YOLOX",
      framework: "Balanced",
      keypoints: "Body",
      computePlatform: "CUDA",
    };

    for (const key in defaultOptions) {
      const group = optionsGroups[key];
      const value = defaultOptions[key];
      const option = [...group.children].find(option => option.dataset.value === value);
      option.classList.add("selected");
      selectedValues[key] = value;
    }

    updateCommand();
  });
</script>