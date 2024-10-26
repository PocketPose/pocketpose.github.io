---
title: Model Zoo
layout: page
description: Trained models for PocketPose.
permalink: "/models/"
---

<div class="container">
    {% for model in site.data.model_zoo %}
        <div class="col-md-12 mb-4">
            <h2>{{ model.name }}</h2>
            <p>{{ model.description }}</p>

            <div class="row">
                {% for variant in model.variants %}
                <div class="col-md-4 mb-4">
                    <div class="card model-card">
                        <div class="card-body">
                            <h5 class="card-title">{{ variant[1].name }}</h5>
                            <p class="card-text">
                                <i class="fa-solid fa-image"></i> {{ variant[1].input_size | join: 'x' }} 
                                <i class="fa-solid fa-diagram-project"></i> {{ variant[1].keypoints }} 
                                <i class="fa-solid fa-compact-disc"></i> {{ variant[1].format }}
                            </p>
                            <a href="{{ variant[1].url }}" class="btn btn-primary" title="Download">
                                <i class="fa-solid fa-cloud-arrow-down"></i>
                            </a>
                            <a href="{{ variant[1].source_url }}" target="_blank" class="btn btn-secondary" title="Original Model">
                                <i class="fa-solid fa-square-arrow-up-right"></i>
                            </a>
                            <a href="{{ variant[1].code }}" target="_blank" class="btn btn-info" title="Code">
                                <i class="fa-brands fa-github"></i>
                            </a>
                        </div>
                        <div class="card-footer">
                            <small><i class="fa-solid fa-code-merge"></i> {{ variant[1].license }}</small>
                        </div>
                    </div>
                </div>
                {% endfor %}
            </div>
        </div>
    {% endfor %}
</div>
