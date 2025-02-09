---
title: "🚀 PocketPose Model Zoo – Pre-Trained Models for Human Pose Estimation"
layout: products
description: "Explore PocketPose Model Zoo – a collection of pre-trained models for human pose estimation optimized for various frameworks and keypoint formats. Perfect for developers and researchers looking to accelerate their pose estimation projects."
permalink: "/models/"
---

# PocketPose Model Zoo – Optimized Pre-Trained Models for Pose Estimation

The __PocketPose Model Zoo__ is your go-to resource for __pre-trained models__ designed for fast, accurate, and efficient __human pose estimation__ across different frameworks and keypoint formats. Whether you’re building real-time applications or conducting advanced research, our models help you __accelerate development__ and __improve accuracy__ without the heavy lifting of training from scratch.

__For Researchers &amp; Developers:__ In addition to our latest high-performance models, we provide access to __legacy pose estimation models__ that have played a pivotal role in the evolution of the field. While these models may not be optimized for speed or accuracy, they remain valuable for __comparative research, benchmarking, and academic exploration__.
{: .note}

For instructions on the latest models, visit our [Get Started](/get-started) page. If you’re looking for a specific model for research or development, use the model explorer below to find the right model for your needs.

<div class="container p-2 mb-4">
  <div class="row">
    <!-- Dropdowns for Filtering -->
    <div class="filter-container">
      <div>
        <label>Backend:</label>
        <div id="frameworkChips" class="chip-container"></div>
      </div>
      <div>
        <label class="mt-2">Skeleton:</label>
        <div id="keypointsChips" class="chip-container"></div>
      </div>
      <div>
        <label class="mt-2">License:</label>
        <div id="licenseChips" class="chip-container"></div>
      </div>
    </div>
    <!-- Models Display -->
    <div id="modelContainer">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Name</th>
            <th>Input Size</th>
            <th>Keypoints</th>
            <th>Format</th>
            <!-- <th>Download</th> -->
            <th>Source</th>
            <th>License</th>
          </tr>
        </thead>
        <tbody>
          {% assign sorted_models = site.data.model_zoo | sort: "name" %}
          {% for model in sorted_models %}
            {% for variant in model.variants %}
            <tr class="model-card-container" data-framework="{{ variant[1].format }}" data-keypoints="{{ variant[1].keypoints }}">
              <td>{{ variant[1].name }}</td>
              <td>{{ variant[1].input_size | join: 'x' }}</td>
              <td>{{ variant[1].keypoints | upcase }}</td>
              <td>{{ variant[1].format | upcase }}</td>
              <!-- <td><a href="{{ variant[1].url }}" class="btn btn-primary" title="Download"><i class="fa-solid fa-cloud-arrow-down"></i></a></td> -->
              <td>
                <a href="{{ variant[1].code }}" target="_blank" title="Source Code">Code</a> &middot;
                <a href="{{ variant[1].source_url }}" target="_blank" title="Source Weights">Weights</a>
              </td>
              <td>{{ variant[1].license }}</td>
            </tr>
            {% endfor %}
          {% endfor %}    </tbody>
      </table>
    </div>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const frameworkSelect = document.getElementById("frameworkSelect");
    const keypointsSelect = document.getElementById("keypointsSelect");
    const licenseSelect = document.getElementById("licenseSelect");
    const modelContainers = document.querySelectorAll(".model-card-container");

    // Extract unique framework formats and keypoints
    let frameworks = new Set();
    let keypoints = new Set();
    let licenses = new Set();

    modelContainers.forEach(card => {
      frameworks.add(card.dataset.framework);
      keypoints.add(card.dataset.keypoints);
      licenses.add(card.querySelector("td:last-child").textContent);
    });

    function createChips(containerId, items) {
      const container = document.getElementById(containerId);
      items.forEach((item, index) => {
        // Skip empty items
        if (!item) return;
        
        const chip = document.createElement("div");
        chip.className = "chip" + (index === 0 ? " selected" : "");
        chip.textContent = item.toUpperCase();
        chip.dataset.value = item;
        container.appendChild(chip);
      });
    }

    createChips("frameworkChips", frameworks);
    createChips("keypointsChips", keypoints);
    createChips("licenseChips", licenses);

    // Filter models based on selections
    function filterModels() {
      const selectedFramework = document.querySelector("#frameworkChips .selected")?.dataset.value;
      const selectedKeypoints = document.querySelector("#keypointsChips .selected")?.dataset.value;
      const selectedLicense = document.querySelector("#licenseChips .selected")?.dataset.value;

      console.log(selectedFramework, selectedKeypoints, selectedLicense);
      modelContainers.forEach(card => {
        const matchesFramework = !selectedFramework || card.dataset.framework === selectedFramework;
        const matchesKeypoints = !selectedKeypoints || card.dataset.keypoints === selectedKeypoints;
        const matchesLicense = !selectedLicense || card.querySelector("td:last-child").textContent === selectedLicense;

        if (matchesFramework && matchesKeypoints && matchesLicense) {
          card.classList.remove("hidden");
        } else {
          card.classList.add("hidden");
        }
      });
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

    setupChips("frameworkChips");
    setupChips("keypointsChips");
    setupChips("licenseChips");

    filterModels();
  });
</script>
