# Project Guidelines

This document outlines the standards, structure, and workflows for this project. It is intended to guide both human developers and AI assistants (like Antigravity) to ensure consistency and maintainability.

## 1. Project Overview

This project is built using the **Cognivac** template, leveraging **Astro 5.0** and **Tailwind CSS**. It is designed for performance, SEO, and ease of customization.

### Tech Stack

- **Framework**: Astro 5.x (`static` output)
- **Styling**: Tailwind CSS 3.4
- **Language**: TypeScript
- **Icons**: `astro-icon` (Tabler, Flat Color Icons)
- **Content**: MDX, Markdown
- **Linting**: ESLint, Prettier

## 2. File Structure & Organization

The `src` directory is organized as follows:

- **`src/assets`**: Images, fonts, and global styles (`styles/tailwind.css`).
- **`src/components`**:
  - **`CustomStyles.astro`**: **CRITICAL**. This file defines the global CSS variables for colors and fonts. Modify this to change the site's theme.
  - **`widgets/`**: High-level page sections (e.g., `Hero`, `Features`, `Content`, `Footer`). Most UI construction should happen here.
  - **`ui/`**: Low-level atomic components (e.g., `Button`, `Form`, `ItemGrid`).
  - **`common/`**: Utilities like `MetaTags`, `Analytics`.
- **`src/layouts`**: Page layouts (`PageLayout`, `Layout`, etc.).
- **`src/pages`**: File-based routing. `.astro` and `.md/.mdx` files here become routes.
- **`src/config.yaml`**: **CRITICAL**. Site metadata, SEO defaults, feature flags (blog, etc.), and UI presets.
- **`src/navigation.ts`**: Defines the links for the Header and Footer.

## 3. Configuration & Customization

### Global Theme (Colors & Fonts)

Do **not** hardcode colors in Tailwind config if they are meant to be themable. Instead, edit **`src/components/CustomStyles.astro`**:

```css
:root {
  --aw-color-primary: rgb(1 97 239);
  --aw-color-bg-page: rgb(255 255 255);
  /* ... */
}
```

These are exposed as Tailwind colors: `primary`, `secondary`, `accent`, `default`, `muted`, `page`.

### Site Metadata

Edit **`src/config.yaml`** to change:

- Site name and URL.
- SEO title templates and descriptions.
- Analytics IDs.
- Feature flags (enable/disable blog).

### Navigation

Edit **`src/navigation.ts`** to modify the Header links and Footer columns.

## 4. Coding Standards

### TypeScript

- Use strict typing.
- Use the `~/` path alias to import from `src`. Example: `import Hero from '~/components/widgets/Hero.astro';`.

### Components

- **Preferred Pattern**: Build pages by composing `widgets`.
- **Props**: Define refined interfaces for props.
- **Images**: Use Astro's `<Image />` component or the project's `Image` adapter where appropriate.

### Styling

- **Tailwind**: Use utility classes for almost everything.
- **Dark Mode**: Supported via the `dark` class. Use `dark:` variants in Tailwind.
- **Responsive**: Use `md:`, `lg:` prefixes. Mobile-first approach.

## 5. Guidelines for Antigravity (AI)

When performing tasks in this codebase, adhere to these rules:

1.  **Check Config First**: Before hardcoding site names or links, check `src/config.yaml` and `src/navigation.ts`.
2.  **Respect The system**: Use the defined CSS variables in `CustomStyles.astro` for strict theming. Do not introduce random hex values for primary/secondary colors.
3.  **Component Hierarchy**: If asked to create a new section, place it in `src/components/widgets`. If it's a small reusable element, place it in `src/components/ui`.
4.  **Icons**: Use `astro-icon`. Example: `<Icon name="tabler:home" />`. Use `tabler` icons by default unless requested otherwise.
5.  **New Pages**: When creating a new page, use the standard layout:

    ```astro
    ---
    import Layout from '~/layouts/PageLayout.astro';
    import Hero from '~/components/widgets/Hero.astro';

    const metadata = { title: 'New Page' };
    ---

    <Layout metadata={metadata}>
      <Hero ... />
    </Layout>
    ```

6.  **Formatting**: Ensure code is Prettier-compliant (single quotes, 2 spaces, semi-colons).

## 6. Common Commands

- `npm run dev`: Start development server.
- `npm run build`: Build for production (`dist/`).
- `npm run preview`: Preview the build.
- `npm run check`: Run type checking and linting.
