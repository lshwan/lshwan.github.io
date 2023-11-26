---
layout: splash
permalink: /
hidden: False
header:
  # overlay_color: "#5e616c"
  # overlay_image: /assets/images/splash.png
  image: /assets/images/splash.png
excerpt: 
intro: 
  - excerpt: "Thank you for visiting my portfolio site.<br /><br />
    I'm Seunghwan Lee, an engineer specializing in Machine Learning, Computer Vision, and Medical AI. In my career as a developer, I have always prioritized:<br /><br />
    <font size=5 color='#5e616c'>End User Satisfaction</font> over system perfection<br />
    <font size=5 color='#5e616c'>Practical Utility</font> over the fanciness of technology<br /><br />
    My approach is rooted in creating solutions that not only advance the field but also deliver tangible benefits to users."
history:
  - image_path: /assets/images/history.svg
    title: "  "
featured_projects:
  - image_path: /assets/images/thumbnail/wound-segmentation.png
    alt: "customizable"
    title: "<font size=3 color='#7f7f7f'><i>#ML #CV #Medical</i></font><br />
            AiD Regen: 2D Diabetic Foot Ulcer Segmentation with HITL"
    excerpt: "<i>Pytorch, OpenCV, FastAPI, GCP Vertex AI, AWS Sagemaker</i>"
    url: "/docs/wound-segmentation/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/mm-customizable-feature.png
    alt: "customizable"
    title: "<font size=3 color='#7f7f7f'><i>#CV #Medical</i></font><br />
            AiD Regen: 3D Bioprintable Patch Generation"
    excerpt: "<i>Open3D, Scipy, Django</i>"
    url: "/docs/comming-soon/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/thumbnail/infusionsurf.png
    alt: "customizable"
    title: "<font size=3 color='#7f7f7f'><i>#ML #CV</i></font><br />
            InFusionSurf: Neural RGB-D Surface Reconstruction"
    excerpt: "<i>Pytorch, Kubeflow, GCP Vertex AI</i>"
    url: "/docs/comming-soon/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
---

{% include feature_row id="intro" type="center" %}

# Career Journey
{% include feature_row id="history" type="teaser" %}

# Featured Projects [<font size=4><i>View more projects</i></font>]({{ "/projects/" | relative_url }})
{% include feature_row id="featured_projects" %}