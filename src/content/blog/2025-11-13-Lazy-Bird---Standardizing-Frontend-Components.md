---
title: "Standardizing Frontend Components"
date:  2025-11-13 23:21:45
categories: ["Lazy Bird Project"]
tags: []
---

## The Problem

As the Lazy Bird project grew to include three different broken systems (Content Delivery, Product Catalog, and Employee Directory), each system implemented its own version of common UI elements. Card containers, loading spinners, error displays, and metrics footers were duplicated across frontends with inconsistent styling and behavior.

This created several issues:
- Inconsistent user experience across systems
- Over 800 lines of duplicated CSS
- Metrics displayed in different formats (seconds vs milliseconds, varying decimal places)

## The Idea: Copy-Based Component Architecture

The key challenge was maintaining system independence while achieving consistency. Each Lazy Bird system needs to work as a standalone Git submodule that users can clone and run independently, without external dependencies.

We considered several approaches:
- **NPM package**: Would create a dependency and complicate standalone usage
- **Git submodules**: Would add complexity and coupling between repositories
- **Monorepo with workspace**: Would eliminate the ability to clone individual systems

Instead, we adopted a **template/source pattern**: create shared components once, then copy them into each system. This approach:
- Preserves system independence (no external dependencies)
- Ensures consistency (same components, same styling)
- Allows system-specific adaptations when needed
- Keeps updates simple (copy new versions when ready)

The trade-off is manual synchronization, but for an educational project, this is manageable and keeps the architecture simple.

## What We Did

### Created the Shared Components Library

Built a centralized library at `/shared/frontend/` containing:

**Components:**
- **SystemLayout**: Enforces Title → Description → Content → Metrics pattern across all systems
- **MetricsFooter**: Standardized metrics display with auto-detection of single vs multiple metrics
- **Card**: Reusable container component with consistent styling
- **LoadingSpinner**: Consistent loading states
- **ErrorDisplay**: Standardized error messages

**Styles:**
- **base.css**: Common styling shared across all systems (layout, typography, buttons, etc.)

### Refactored Three Systems

We applied the standardized components to all existing systems:

**Content Delivery System**
- Before: 303 lines of CSS
- After: 69 lines of system-specific CSS
- Reduction: 234 lines (77%)

**Product Catalog System**
- Before: 258 lines of CSS
- After: 24 lines of system-specific CSS
- Reduction: 234 lines (91%)

**Employee Directory System**
- Before: 261 lines of CSS
- After: 134 lines of system-specific CSS
- Reduction: 127 lines (49%)

### Standardized Metrics

All systems now display performance metrics consistently:
- **Format**: Milliseconds with no decimal places (using `Math.round()`)
- **Timing**: Frontend-driven using `Date.now()`
- **Display**: Single metrics show inline, multiple metrics display as a grid

## Tutorial: Adding Shared Components to a New System

Follow these steps to add the standardized components when building a new Lazy Bird system:

### Step 1: Copy Shared Components

From your system's frontend directory:

```bash
# Create directories for shared code
mkdir -p src/shared-components
mkdir -p src/shared-styles

# Copy components from shared library
cp -r /path/to/lazy-bird/shared/frontend/src/components/* src/shared-components/
cp -r /path/to/lazy-bird/shared/frontend/src/styles/* src/shared-styles/
```

### Step 2: Import Shared Styles

Update your `src/index.tsx` or `src/index.jsx` to import base styles:

```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import "./shared-styles/base.css";  // Add this line
import "./index.css";
import App from "./App";
```

### Step 3: Ensure TypeScript Configuration

Make sure your frontend has a `tsconfig.json` file. If missing, create one:

```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"]
}
```

This enables clean imports without `.tsx` file extensions.

### Step 4: Build Your Main Component

Structure your main component to use SystemLayout:

```typescript
import { SystemLayout } from '../../shared-components/SystemLayout';
import { MetricsFooter } from '../../shared-components/MetricsFooter';

const MyComponent: React.FC = () => {
  return (
    <SystemLayout
      title="My System"
      description={<p>System description...</p>}
      loading={isLoading}
      error={errorMessage}
      metrics={
        loadTime ? (
          <MetricsFooter
            metrics={[
              { label: 'Load Time', value: loadTime, unit: 'ms' }
            ]}
          />
        ) : undefined
      }
    >
      {/* Your system-specific content here */}
    </SystemLayout>
  );
};
```

Your `App.css` should only contain system-specific styles (custom components, unique layouts, etc.). All common styles are already in `base.css`.

### Step 5: Standardize Metrics

Ensure all performance measurements use milliseconds:

```typescript
// Measure time in milliseconds
const startTime = Date.now();
// ... operation ...
const endTime = Date.now();
const duration = endTime - startTime;  // Already in ms

// Display with MetricsFooter (automatically rounds)
<MetricsFooter
  metrics={[
    { label: 'Total Time', value: duration, unit: 'ms' }
  ]}
/>
```

### Step 6: Rebuild and Test

```bash
# Rebuild containers to pick up new files
make clean && make build

# Verify compilation
docker logs <your-system>_frontend
```

You should see "Compiled successfully!" with no errors.

## Conclusion

This refactoring demonstrates that consistency doesn't require complex build systems. By embracing a simple copy-based architecture, the project achieved significant improvements:

**Code Reduction**
- Total CSS removed: ~595 lines across three systems
- Average reduction: 72% decrease in system-specific CSS
- Each system now contains only unique, system-specific styles

**Performance**
- Reduced bundle size with less duplicated CSS
- Faster development with reusable components

**Code Quality**
- Single source of truth for common patterns
- Clear separation between shared and system-specific styles
- TypeScript interfaces prevent prop errors
- Consistent behavior across all systems

**Maintainability**
- New contributors see consistent patterns across all systems
- System independence preserved for educational use

The Lazy Bird project now has a solid foundation for adding new systems while maintaining a consistent, professional user experience. Users working with these systems see real-world examples of component reusability and design system thinking in action.

---
