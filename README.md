# Exoscale Academy

Welcome to **Exoscale Academy**, the dedicated cloud education and training platform powered by Layer5. This repository provides a comprehensive framework for creating, organizing, and publishing structured learning paths, courses, and lessons tailored for Exoscale users and cloud practitioners.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Repository Structure](#repository-structure)
- [Content Authoring Workflow](#content-authoring-workflow)
- [Managing Assets: Images, Videos, and Embedded Designs](#managing-assets-images-videos-and-embedded-designs)
- [Local Development](#local-development)
- [Deploying & Going Live](#deploying--going-live)
- [Contributing](#contributing)
- [Site Framework](#site-framework)
- [License](#license)

## Prerequisites

Before you begin, ensure you have:

- [**Hugo**](https://gohugo.io/getting-started/installing/) (extended version, recommended v0.147.9 or later)
- [**Go**](https://go.dev/doc/install) (v1.12 or later)

## Getting Started

1. **Clone the Repository**

   ```bash
   git clone https://github.com/layer5io/exoscale-academy.git
   cd exoscale-academy
   ```

2. **(Optional: If contributing from a fork)**
   - Edit `go.mod` and update the module path to match your fork. Save and commit.

3. **Organization UID**
   - All Exoscale Academy content is namespaced under the UID:
     ```
     98e16360-a366-4b78-8e0a-031da07fdacb
     ```

## Repository Structure

```
layer5io-exoscale-academy/
├── README.md
├── LICENSE
├── go.mod, go.sum
├── hugo.yaml
├── Makefile, flake.nix, flake.lock, package.json, postcss.config.js
├── content/
│   └── en/
│       └── learning-paths/
│           └── 98e16360-a366-4b78-8e0a-031da07fdacb/
│               └── /
│                   └── /
│                       └── /
│                           └── content/
│                               └── .md
├── static/
│   └── 98e16360-a366-4b78-8e0a-031da07fdacb/
│       └── images/
├── layouts/
│   └── shortcodes/
│       └── 98e16360-a366-4b78-8e0a-031da07fdacb/
│           └── custom-org-shortcode.html
└── .github/
    └── ISSUE_TEMPLATE/, workflows/, config, etc.
```
> **Learning Path → Course → Chapter → Lesson** is the core structure.  
Each level uses `_index.md` and lessons use `.md` files with [Hugo frontmatter](https://gohugo.io/content-management/front-matter/).

## Content Authoring Workflow

1. **Create Content**

   - Authoring takes place inside:
     ```
     content/en/learning-paths/98e16360-a366-4b78-8e0a-031da07fdacb/
     ```
   - Structure:
     ```
     <learning-path>/
      <course>/
        <chapter>/
            content/
              lesson1.md
              lesson2.md
     ```

   - **Frontmatter Required** (example for any `_index.md` or lesson .md):

     ```yaml
     ---
     title: "Title of Section or Lesson"
     description: "One-liner summary"
     weight: 10  # for menu order, lower numbers appear first
     ---
     ```

2. **Delete Example Content**
   - Remove any demo/example files not relevant to your new material.

3. **Organize Lessons**
   - Add new folders and markdown files for each learning path, course, chapter, and lesson.

## Managing Assets: Images, Videos, and Embedded Designs

Enhance your courses with images and rich visual content. For compatibility with the Layer5 Academy’s multi-tenant architecture, **do not use standard Markdown image links**. Use shortcodes as described below.

### How to Add an Image

1. Place your image (example: `exoscale-logo.png`) in the organization’s static directory:

    ```
    static/98e16360-a366-4b78-8e0a-031da07fdacb/images/exoscale-logo.png
    ```

2. In lesson markdown, embed your image using the `usestatic` shortcode (path is relative to your org’s folder):

    ```markdown
    ![Exoscale Logo]({{</* usestatic path="images/exoscale-logo.png" */>}})
    ```

> When you build the site, this shortcode automatically resolves to a working, tenant-aware asset path.

### How to Add a Video

Embed videos in a visually distinct `card` using:

```markdown
{{</* card title="Video: Example" */>}}
<video width="100%" height="100%" controls>
    <source src="https://example.com/your-video.mp4" type="video/mp4">
    Your browser does not support the video tag.
</video>
{{</* /card */>}}
```
## How to Add a Meshery Design

1. Place Design Assets  
   Put your design files (e.g., `cdn.js`, design YAMLs) alongside your course or lesson content, ideally following the same directory conventions used for images.

2. Embed Using the meshery-design-embed Shortcode  
   In your lesson markdown, use:
  
  ```markdown
  {{< meshery-design-embed
  id="embedded-design-0e3abb9c-39e7-4d09-b46f-26a0238c3c3d"
  src="cdn.js"
  >}}
  ```

   - Replace `id` with the unique identifier for your design.
   - Replace `src` with the path to your JS asset responsible for rendering.

> Always use these shortcodes for images, videos, and embedded designs. This keeps assets portable, ensures they resolve correctly for each organization, and integrates properly with the Academy platform’s build and deployment flow.

## Local Development

To preview your content locally, run:

```bash
hugo server
```

- Open the local URL displayed in your terminal browser.
- Local preview uses plain styling; full Layer5 Cloud branding is applied on production.

## Deploying & Going Live

1. **Commit and push** your changes to a branch or `main`.
2. **Contact Layer5** via [Slack](https://slack.layer5.io/), email, or by opening a GitHub issue.
3. Provide your repository URL.
4. Once reviewed, a Layer5 admin will synchronize your content to the [Layer5 Cloud Academy](https://cloud.layer5.io/academy/overview).

## Contributing

- See [Academy Docs](https://docs.layer5.io/cloud/academy) for best practices on creating and publishing learning paths, courses, chapters, and challenges.
- Refer to [CONTRIBUTING.md](./CONTRIBUTING.md) for branching, committing, and PR workflow.
- Review [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) and [SECURITY.md](./SECURITY.md) prior to contributing.

## Site Framework

- **Stack:** Built with [Golang](https://golang.org/) and [Hugo](https://gohugo.io/), fully integrated with [Layer5 Cloud](https://cloud.layer5.io/academy/overview).
- **Theme & Template:** Refer to [academy-theme](https://github.com/layer5io/academy-theme) and [academy-template](https://github.com/layer5io/academy-template) for advanced customization.

## License

Distributed under the [Apache 2.0 License](./LICENSE).

For questions or help, open a [GitHub Issue](https://github.com/layer5io/exoscale-academy/issues) or join the [Layer5 Slack Community](https://slack.layer5.io/).

**Happy Learning!**  
_The Layer5 & Exoscale Academy Team_
