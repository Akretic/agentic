# TypeScript Conventions

> Applies to all TypeScript/JavaScript projects managed by this pipeline.

---

## Imports

Order imports in this sequence, separated by blank lines:

1. Node/framework imports (`react`, `next`, `@nestjs/*`)
2. Third-party libraries (`@tanstack/react-query`, `zod`, `axios`)
3. Internal packages (workspace imports, shared libraries)
4. Local imports (`@/lib/*`, `@/components/*`)
5. Type-only imports (`import type { ... }`)

```typescript
import { Controller, Get } from '@nestjs/common';
import { useQuery } from '@tanstack/react-query';

import type { Project } from '@internal/domain';

import { apiClient } from '@/lib/api';
import { logger } from '@/lib/logger';

import type { PageProps } from './types';
```

## Types

- **No `any`.** Use `unknown` if the type is genuinely unknown, then narrow.
- **No type assertions (`as`)** unless there is no alternative. Add a comment explaining why.
- **Prefer `interface` for object shapes**, `type` for unions and computed types.
- **Export types separately** from runtime values: `export type { ... }`.

## Error Handling

```typescript
// ✅ Always
try {
  await apiClient.projects.create(data);
} catch (error) {
  logger.error('Failed to create project', error, { formData: data });
  throw error; // or handle gracefully in UI
}

// ❌ Never
console.error('Error:', error);
```

## Components (React)

- One component per file.
- File name matches component name: `ProjectCard.tsx` → `export function ProjectCard`.
- Props interface defined at the top of the file, not inline.
- Use `useCallback` for event handlers passed to children.
- Use `useMemo` for derived/filtered data.

```typescript
interface ProjectCardProps {
  project: Project;
  onDelete: (id: string) => void;
}

export function ProjectCard({ project, onDelete }: ProjectCardProps) {
  const handleDelete = useCallback(() => {
    onDelete(project.id);
  }, [project.id, onDelete]);

  return (/* ... */);
}
```

## API Patterns

- **Backend (NestJS/Express/Fastify, if applicable):** controller handles HTTP, service handles logic, ORM handles data.
- **Frontend:** use React Query (or project-specific data layer) for all data fetching. No raw `fetch` or `axios` calls.
- **Mutations:** always invalidate related queries on success.
- **Paginated responses:** API client handles `{ data, meta }` extraction automatically.

## Naming

| Thing | Convention | Example |
|-------|-----------|---------|
| Files (component) | PascalCase | `ProjectCard.tsx` |
| Files (utility) | camelCase | `apiClient.ts` |
| Files (page) | `page.tsx` in directory | `app/projects/page.tsx` |
| Variables | camelCase | `projectCount` |
| Constants | UPPER_SNAKE | `MAX_FILE_SIZE` |
| Types/Interfaces | PascalCase | `ProjectStatus` |
| Enums | PascalCase members | `Status.Active` |
| CSS classes | Per-project convention (Tailwind, CSS Modules, vanilla CSS, etc.) | — |

## Testing

- Test files live in `__tests__/` directories mirroring source structure.
- Mock API client, not HTTP layer.
- Wrap components in `QueryClientProvider` with `retry: false`.
- Test accessibility: use `getByRole`, `getByLabelText` over `getByTestId`.
