---
title: "🚀 PocketPose Model Zoo – Free Pre-Trained Models for Human Pose Estimation"
layout: page
description: "Explore the PocketPose Model Zoo – a comprehensive collection of free, high-performance pre-trained models for 2D and 3D human pose estimation. Optimized for various frameworks and keypoint formats, our models help developers and researchers accelerate pose estimation projects with ease."
keywords: "human pose estimation, pose estimation models, pre-trained pose estimation models, 2D pose estimation, 3D pose estimation, deep learning pose estimation, skeleton tracking, keypoint detection, pose estimation AI, open-source pose models, PocketPose models"
permalink: "/models/"
---

Welcome to the **PocketPose Model Zoo**, your ultimate resource for **pre-trained models** designed for **fast, accurate, and efficient human pose estimation** across a variety of **frameworks and keypoint formats**. Whether you're building **real-time applications** or conducting **cutting-edge research**, our models provide **high-performance solutions** without the hassle of training from scratch.  

For minimal setup with automatic selection of the best model for your use case, visit our [Get Started](/get-started) page.

__For Researchers &amp; Developers:__ Alongside the latest **high-performance pose estimation models**, we provide access to **legacy models** that played a pivotal role in shaping the field. These older models are ideal for __comparative research, benchmarking, and academic exploration__.
{: .note}

Use our interactive **Model Explorer** below to filter and discover all available models in the PocketPose Model Zoo.  

<div class="container model-selector filter-container">
  <!-- Dropdowns for Filtering -->
  <div class="row px-2">
    <label class="selector-header">Pipeline:</label>
    <div id="pipelineChips" class="options-grid chip-container"></div>
  </div>
  <div class="row px-2">
    <label class="selector-header">Skeleton:</label>
    <div id="keypointsChips" class="options-grid chip-container"></div>
  </div>
  <div class="row px-2">
    <label class="selector-header">Backend:</label>
    <div id="frameworkChips" class="options-grid chip-container"></div>
  </div>
  <div class="row px-2">
    <label class="selector-header">License:</label>
    <div id="licenseChips" class="options-grid chip-container"></div>
  </div>

  <!-- Models Display -->
  <div id="modelContainer" class="table-responsive">
    <table class="table table-bordered table-striped">
      <caption>
        <div id="modelCount" style="font-weight: bold;"></div>
        <div>* Reported Metrics: COCO AP for 2D models using COCO/COCO-WholeBody keypoints, PCKh for 2D models with MPII keypoints, and MPJPE for 3D models. Metrics are evaluated on validation datasets using the same person detector (RTMDet) where applicable. Higher values indicate better performance.
        </div> 
        <div>** Speed: Measured on a 2024 MacBook Pro 14” (M4 Pro) using ONNX Runtime. Lower values indicate better performance.</div>
      </caption>
      <thead class="thead-dark">
        <tr>
          <th>Name</th>
          <th>Input Size</th>
          <th>Keypoints</th>
          <th>Size (MB)</th>
          <th>Accuracy*</th>
          <th>Speed (FPS)**</th>
          <th>Backend</th>
          <th>Source</th>
          <th>License</th>
        </tr>
      </thead>
      <tbody>
        {% assign sorted_models = site.data.model_zoo | sort: "year" | reverse %}
        {% for model in sorted_models %}
          {% if model.type == "detectors" %}
            {% continue %}
          {% endif %}
          <tr class="model-card-header" data-group="{{ model.name }}">
            <td colspan="9" style="text-align: center;">
              <b><a href="{{ model.paper }}" target="_blank">{{ model.name }}</a> ({{ model.year }})</b> <br>
              {{ model.pipeline }} <b>|</b> {{ model.backbone }} <b>|</b> {{ model.head }}
            </td>
          </tr>
          {% for variant in model.variants %}
          <tr class="model-card-container" data-group="{{ model.name }}"
            data-pipeline="{{ model.pipeline }}"
            data-keypoints="{{ variant[1].keypoints }}"
            data-framework="{{ variant[1].format }}" 
            data-license="{{ variant[1].license }}">
            <td>{{ variant[1].name }}</td>
            <td>{{ variant[1].input_size | join: 'x' }}</td>
            <td>{{ variant[1].keypoints | upcase }}</td>
            <td>{{ variant[1].file_size }}</td>
            <td>{{ variant[1].performance }}</td>
            <td>{{ variant[1].latency }}</td>
            <td>{{ variant[1].format | upcase }}</td>
            <td>
              {{variant[1].source}}:
              {% if variant[1].code != "" %}
              <a href="{{ variant[1].code }}" target="_blank" title="Source Code">Code</a> &middot;
              {% endif %}
              <a href="{{ variant[1].source_url }}" target="_blank" title="Original Weights">Weights</a>
            </td>
            <td>{{ variant[1].license }}</td>
          </tr>
          {% endfor %}
        {% endfor %}    
      </tbody>
    </table>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const pipelineSelect = document.getElementById("pipelineSelect");
    const keypointsSelect = document.getElementById("keypointsSelect");
    const frameworkSelect = document.getElementById("frameworkSelect");
    const licenseSelect = document.getElementById("licenseSelect");

    const modelContainers = document.querySelectorAll(".model-card-container");

    // Extract unique framework formats and keypoints
    let pipelines = new Set();
    let frameworks = new Set();
    let keypoints = new Set();
    let licenses = new Set();

    modelContainers.forEach(card => {
      pipelines.add(card.dataset.pipeline);
      frameworks.add(card.dataset.framework);
      keypoints.add(card.dataset.keypoints);
      licenses.add(card.querySelector("td:last-child").textContent);
    });

    // Sort sets to ensure consistent order
    pipelines = Array.from(pipelines).sort();
    frameworks = Array.from(frameworks).sort();
    keypoints = Array.from(keypoints).sort();
    licenses = Array.from(licenses).sort();

    function createChips(containerId, items) {
      const container = document.getElementById(containerId);
      items.forEach((item, index) => {
        // Skip empty items
        if (!item) return;
        
        const chip = document.createElement("div");
        chip.className = "option chip"; // + (index === 0 ? " selected" : "");
        chip.textContent = item.toUpperCase();
        chip.dataset.value = item;
        container.appendChild(chip);
      });
    }

    createChips("pipelineChips", pipelines);
    createChips("frameworkChips", frameworks);
    createChips("keypointsChips", keypoints);
    createChips("licenseChips", licenses);

    // Filter models based on selections
    function filterModels() {
      const selectedPipeline = document.querySelector("#pipelineChips .selected")?.dataset.value;
      const selectedFramework = document.querySelector("#frameworkChips .selected")?.dataset.value;
      const selectedKeypoints = document.querySelector("#keypointsChips .selected")?.dataset.value;
      const selectedLicense = document.querySelector("#licenseChips .selected")?.dataset.value;

      let visibleModels = 0; // Counter for the number of visible model variants

      document.querySelectorAll(".model-card-container").forEach(card => {
        const matchesPipeline = !selectedPipeline || card.dataset.pipeline === selectedPipeline;
        const matchesFramework = !selectedFramework || card.dataset.framework === selectedFramework;
        const matchesKeypoints = !selectedKeypoints || card.dataset.keypoints === selectedKeypoints;
        const matchesLicense = !selectedLicense || card.dataset.license === selectedLicense;

        if (matchesPipeline && matchesFramework && matchesKeypoints && matchesLicense) {
          card.classList.remove("hidden");
          visibleModels++;
        } else {
          card.classList.add("hidden");
        }
      });

      // Hide group headers when all their variants are hidden
      document.querySelectorAll(`.model-card-header`).forEach(group => {
        const groupName = group.dataset.group;
        const groupModels = document.querySelectorAll(`.model-card-container[data-group="${groupName}"]:not(.hidden)`);

        if (groupModels.length === 0) {
          group.classList.add("hidden");
        } else {
          group.classList.remove("hidden");
        }
      });

      // Update model count
      document.getElementById("modelCount").textContent = `Showing ${visibleModels} matching models`;
    }

    // Setup chip selection
    function setupChips(containerId) {
      const container = document.getElementById(containerId);
      container.addEventListener("click", function (event) {
        if (event.target.classList.contains("chip")) {
          [...container.children].forEach(chip => {
            if (chip !== event.target) {
              chip.classList.remove("selected");
            }
          });
          event.target.classList.toggle("selected");
          filterModels();    }
      });
    }

    setupChips("pipelineChips");
    setupChips("frameworkChips");
    setupChips("keypointsChips");
    setupChips("licenseChips");

    filterModels();
  });
</script>
