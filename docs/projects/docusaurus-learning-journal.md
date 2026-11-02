# Docusaurus Learning Journal

This project documents the setup and customization of my personal developer portfolio and learning journal using [Docusaurus](https://docusaurus.io/).

The website is based on the Developer Akademie Docusaurus template and serves as a platform to document my projects, share development experiences, and publish blog posts.

## TOC

- [Quickstart](#quickstart)
- [Description](#description)
  - [Project Setup](#project-setup)
  - [Website Configuration](#website-configuration)
  - [Environment Variables](#environment-variables)
  - [Navigation and Footer](#navigation-and-footer)
  - [Deployment](#deployment)
  - [Lessons Learned](#lessons-learned)
- [Further References](#further-references)

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition
    link="https://github.com/tofa93/my-dso-blog"
    title="GitHub Repository"
    type="tip"
>
Check out my GitHub repository to see the source code and implementation of this project.
</GithubLinkAdmonition>

## Quickstart

To run this project locally, follow these steps:

1. Clone the repository:

   ```bash
   git clone https://github.com/tofa93/my-dso-blog.git
   cd my-dso-blog
   ```

2. Install the required dependencies:

   ```bash
   npm install
   ```

3. Create a local `.env` file based on `example.env`:

   ```powershell
   Copy-Item example.env .env
   ```

4. Start the development server:

   ```bash
   npm start
   ```

5. Build the website:

   ```bash
   npm run build
   ```

The development server automatically reloads the website when changes are made.

## Description

### Project Setup

I started this project using the Docusaurus starter template provided by the Developer Akademie.

The main goal was to transform the template into a personal developer portfolio and learning journal.

For the implementation, I created a feature branch named `setup-blog` to keep my configuration changes separate from the main branch.

### Website Configuration

The main configuration is located in `docusaurus.config.ts`.

I customized the following properties:

- **Title:** Portfolio of Tommy Falk
- **Tagline:** Tommy Falk - Software Developer, DevSecOps Enthusiast, Blogger
- **Navbar Title:** Portfolio Tommy Falk
- **Logo:** Custom Tofa93 logo
- **Default URL:** https://tofa93.github.io

I also replaced the default template references with links to my own GitHub repository.

### Environment Variables

The project uses `dotenv` to manage environment variables.

I added `GIT_REPOSITORY_URL` to the `example.env` file and configured Docusaurus to read this value.

```typescript
const gitRepositoryUrl =
  process.env.GIT_REPOSITORY_URL ||
  'https://github.com/tofa93/my-dso-blog.git';
```

This variable is used for the repository links and the `editUrl` configuration of the documentation and blog.

Other environment variables control the deployment URL, base URL, GitHub organization, and project name.

### Navigation and Footer

I customized the navigation bar and footer to match my personal portfolio.

The following changes were made:

- Updated the navigation title.
- Added my custom Tofa93 logo.
- Updated the GitHub repository links.
- Added a Projects link to the documentation section.
- Removed the default Community section.
- Added a reference to the original template repository.
- Personalized the copyright message.

The copyright message also includes the attribution:

`extended from the developer-akademie-starter`

### Deployment

The website uses GitHub Actions for automated deployment to GitHub Pages.

A prepared workflow automatically builds and deploys the website whenever a commit is pushed to the `main` branch.

The deployment configuration is located in:

- `.github/workflows/main.yml`
- `.github/workflows/deploy.yaml`

GitHub Pages must be configured to use GitHub Actions as its deployment source.

### Lessons Learned

During this project, I gained experience with:

- Configuring and customizing Docusaurus.
- Working with TypeScript configuration files.
- Managing environment variables using `dotenv`.
- Customizing website navigation and branding.
- Creating documentation using Markdown.
- Working with Git branches and commits.
- Understanding automated deployment using GitHub Actions.
- Troubleshooting TypeScript configuration issues.

This project helped me understand how a static website can be configured, maintained, and automatically deployed using modern development tools.

## Further References

- [My GitHub Repository](https://github.com/tofa93/my-dso-blog)
- [Developer Akademie Template](https://github.com/Developer-Akademie-DevSecOpsKurs/dev-blog-template)
- [Docusaurus Documentation](https://docusaurus.io/docs)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
